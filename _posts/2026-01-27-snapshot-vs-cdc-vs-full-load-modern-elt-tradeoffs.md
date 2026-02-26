---
layout: post
title: "Snapshot vs CDC vs Full-Load: A Practical Modeling Tradeoff in Modern ELT"
date: 2026-01-27
categories: data-engineering architecture elt snowflake
---

# Snapshot vs CDC vs Full-Load: A Practical Modeling Tradeoff in Modern ELT

One of the most misunderstood topics in modern data engineering is incremental loading strategy.

Teams often jump to Change Data Capture (CDC) assuming it is automatically superior. Others rely on daily snapshots without understanding the tradeoffs. Some insist on full production loads for “correctness.”

The reality is more nuanced.

In this article, I’ll break down the architectural tradeoffs between Snapshot-based loads, CDC pipelines, and Full-load staging models — and when each is appropriate.

---

## The Three Loading Strategies

### 1. Full Production Load

Definition:

Load the entire source table into staging on every run.

Characteristics:

- Simple logic
- No watermark tracking
- High compute cost
- High data movement

Benefits:

- Strong correctness guarantees
- Handles late-arriving updates naturally
- Easy recovery from failed runs

Drawbacks:

- Expensive at scale
- Slow for large tables
- Operationally inefficient

This model works well for small datasets or low-frequency pipelines.

It does not scale well for high-volume transactional systems.

---

### 2. Windowed Snapshot / Incremental Load

Definition:

Load records modified within a time window using offset and delta logic.

Example conceptual approach:

    modified_datetime >= current_run_time - delta_hours
    AND modified_datetime < current_run_time - offset_hours

Where:
- offset protects against source lag
- delta creates overlapping safety window

Benefits:

- Cost-efficient
- Scales well
- Easier to implement than CDC
- Works well when source uses soft deletes

Drawbacks:

- Requires careful window tuning
- Potential gaps if runs are missed
- Must design for idempotency

This is often the most practical solution in healthcare analytics environments.

---

### 3. Change Data Capture (CDC)

Definition:

Capture row-level inserts, updates, and deletes directly from source logs.

Typically implemented via:

- Log-based replication
- Database binlog readers
- Streaming connectors

Benefits:

- Near real-time updates
- Precise change tracking
- Handles deletes explicitly
- Minimal reprocessing

Drawbacks:

- Complex setup
- Higher operational overhead
- Requires deeper source system integration
- Harder to debug

CDC is powerful — but not always necessary.

---

## The Real Question: What Does the Business Require?

Many engineering debates focus on theoretical correctness.

The correct question is:

What level of freshness and historical fidelity does the business actually need?

For example:

- If dashboards only display data up to T-1 day,
- If source systems use soft deletes,
- If business KPIs do not rely on intra-day changes,

Then full CDC may provide minimal incremental value.

Architecture should align with business requirements — not engineering perfection.

---

## Late-Arriving Data

One of the strongest arguments for CDC is late-arriving updates.

However, windowed incremental models can handle this if:

- The delta window overlaps sufficiently
- The ETL runs daily
- Modified timestamps are reliable

Example safe configuration:

- ETL runs at 4:00 AM daily
- Offset = 4 hours
- Delta = 30 hours

This ensures overlap with prior loads and prevents missed updates.

Designing the window properly is more important than blindly adopting CDC.

---

## Hard Deletes vs Soft Deletes

This is a major decision factor.

If the source performs hard deletes:

- Snapshot or incremental logic may miss deleted rows
- CDC is strongly recommended

If the source performs soft deletes:

- Modified timestamps capture record state changes
- Windowed incremental loads remain sufficient

Understanding delete behavior is critical before choosing architecture.

---

## Idempotency & Recovery

Regardless of load strategy, pipelines must be idempotent.

That means:

- Re-running the same load does not corrupt data
- MERGE statements handle duplicates correctly
- Primary keys are enforced
- Watermarks are stored safely

If your incremental logic is not idempotent, CDC will not save you.

Correctness is a modeling discipline — not just a pipeline choice.

---

## Cost vs Operational Complexity

Let’s compare realistically.

Full Load:
- Low complexity
- High cost

Windowed Incremental:
- Medium complexity
- Low cost
- High practicality

CDC:
- High complexity
- Medium cost
- Maximum granularity

In most analytics platforms, windowed incremental models strike the best balance.

CDC becomes compelling when:

- Real-time dashboards are required
- Hard deletes exist
- Regulatory audit trails demand change history
- Streaming architecture is already in place

---

## When CDC Is Over-Engineering

CDC is unnecessary when:

- Dashboards are daily refresh
- No business KPI depends on intra-day record mutation
- Data volume is manageable via incremental windows
- Operational team is small

Engineering maturity includes knowing when not to overbuild.

---

## A Practical Decision Framework

Ask these questions:

1. What is the required data freshness SLA?
2. Does the source system perform hard deletes?
3. Is modified_datetime reliable?
4. What is expected data growth over 3 years?
5. What is the team’s operational capacity?
6. Do downstream models require full change history?

Only after answering these should CDC be considered.

---

## Final Perspective

There is no universally superior loading strategy.

There is only:

- Alignment with business needs
- Proper risk mitigation
- Cost awareness
- Operational realism

Modern ELT is not about chasing the most advanced architecture.

It is about designing the most appropriate one.

That discipline separates system builders from tool users.
