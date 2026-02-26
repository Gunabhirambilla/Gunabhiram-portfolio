---
layout: post
title: "Building Idempotent ETL Pipelines in Snowflake + Python"
date: 2026-02-05
categories: data-engineering snowflake python reliability
---

# Building Idempotent ETL Pipelines in Snowflake + Python

In production data systems, failures are not hypothetical — they are guaranteed.

Network interruptions happen. Source systems delay updates. Jobs crash mid-run. Warehouses suspend unexpectedly. Engineers redeploy pipelines.

The difference between a fragile pipeline and a production-grade one is idempotency.

Idempotent pipelines ensure that running the same job multiple times produces the same result without duplication, corruption, or drift.

In this article, I’ll walk through how I design idempotent ETL pipelines using Snowflake and Python.

---

## What Does Idempotency Actually Mean?

A pipeline is idempotent when:

- Re-running the same batch does not create duplicate records
- Partial failures can be safely retried
- Data consistency is preserved across reruns
- Load windows can overlap safely

Idempotency is not a feature — it is a discipline enforced at multiple layers.

---

## Core Design Principles

There are five core principles I follow.

1. Deterministic Load Windows  
2. Explicit Primary Keys  
3. MERGE-Based Upserts  
4. Safe Watermark Management  
5. Atomic Write Patterns  

Let’s break each down.

---

## 1. Deterministic Load Windows

Incremental pipelines should load based on a predictable window.

Example logic:

    modified_datetime >= last_successful_run
    AND modified_datetime < current_run_cutoff

Key design rule:

Never use “now()” directly in transformation logic. Always compute a fixed cutoff timestamp at the start of the job and reuse it consistently.

This ensures reruns operate on the exact same dataset.

---

## 2. Explicit Primary Keys

Every fact table must have a clearly defined business key.

Example:

    appointment_id + practice_id

Never rely on surrogate row numbers or ingestion order.

Primary keys must:

- Represent true entity uniqueness
- Be stable across reruns
- Be enforced via constraint or validation

Without deterministic keys, idempotency collapses.

---

## 3. MERGE Instead of INSERT

Snowflake’s MERGE statement is the backbone of idempotent loads.

Pattern:

- Match on business key
- Update when matched
- Insert when not matched

Conceptually:

    MERGE INTO target_table t
    USING staging_table s
    ON t.business_key = s.business_key
    WHEN MATCHED THEN UPDATE
    WHEN NOT MATCHED THEN INSERT

This ensures:

- Duplicate loads do not create extra rows
- Updated records overwrite prior versions safely
- Retry logic becomes safe

Never use raw INSERT for incremental production loads.

---

## 4. Safe Watermark Management

Watermarks track progress in incremental pipelines.

Common mistake:

Updating watermark before confirming successful load.

Correct pattern:

1. Compute cutoff timestamp
2. Extract and stage data
3. Successfully MERGE into target
4. Validate row counts
5. Only then update watermark

Watermarks should be stored in a dedicated control table:

    pipeline_name
    last_successful_run_timestamp
    status
    row_count_loaded

This enables:

- Observability
- Debugging
- Safe recovery

---

## 5. Atomic Write Patterns

Avoid partially written tables.

Best practices:

- Load into temporary or staging tables first
- Validate row counts
- Perform MERGE into target
- Commit only after validation

In Python orchestration:

- Wrap database calls in transactions
- Fail fast on errors
- Do not swallow exceptions

Partial success is worse than full failure.

---

## Handling Overlapping Windows

Many production systems use overlapping delta windows for safety.

Example:

- ETL runs daily at 4:00 AM
- Delta window = 30 hours
- Offset = 4 hours

This intentionally overlaps prior loads.

Idempotency ensures overlapping records do not cause duplication.

Without MERGE logic, overlap becomes a bug.

With idempotent design, overlap becomes protection.

---

## Delete Handling Strategy

Deletes require special consideration.

If source uses soft deletes:

- Include deleted_flag in staging
- Update target records accordingly

If source uses hard deletes:

- Maintain delete detection logic
- Compare source vs target keys
- Mark missing records as deleted

Deletes must be deterministic.

Otherwise reruns create inconsistency.

---

## Failure Recovery Scenarios

Let’s examine common failure cases.

Case 1: Job crashes before MERGE  
Safe. Rerun loads same staging window.

Case 2: Job crashes after MERGE but before watermark update  
Safe. MERGE prevents duplication.

Case 3: Job crashes mid-MERGE  
Handled via transaction rollback.

If your design cannot safely handle these cases, it is not idempotent.

---

## Observability Layer

Idempotent systems require visibility.

Track:

- Rows extracted
- Rows merged
- Rows updated
- Rows inserted
- Rows deleted
- Execution duration
- Query IDs for debugging

Snowflake’s QUERY_HISTORY view is extremely useful for validation and auditing.

---

## Common Anti-Patterns

Avoid these:

- Using INSERT INTO SELECT without key matching
- Updating watermark before load validation
- Relying on ingestion timestamp instead of source modified timestamp
- Swallowing exceptions in Python orchestration
- Mixing business transformation logic with extraction logic

These patterns break reliability.

---

## Why Idempotency Matters at Scale

As data volume grows:

- Reruns become common
- Backfills become necessary
- Schema changes occur
- Late-arriving data increases

Without idempotent design, each of these becomes an incident.

With idempotency, they become routine operations.

---

## Final Takeaway

Idempotency is not optional in modern data engineering.

It is the foundation of:

- Reliable incremental pipelines
- Safe retries
- Cost-efficient overlapping windows
- Scalable architecture

Anyone can build a pipeline that works once.

A data engineer builds pipelines that survive failure.

That distinction defines production maturity.
