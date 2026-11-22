---
title: "Not All Analytics Are Equal: Benchmarking Databases for Real-Time Analytics Applications"
date: 2025-03-26
publication: Tiger Data blog
original_url: https://www.tigerdata.com/blog/benchmarking-databases-for-real-time-analytics-applications
canonical_url: https://www.tigerdata.com/blog/benchmarking-databases-for-real-time-analytics-applications
sitemap: false
archive_url: https://web.archive.org/web/20260812114022/https://www.tigerdata.com/blog/benchmarking-databases-for-real-time-analytics-applications
description: "Not all analytics are equal—neither are benchmarks. Meet RTABench and compare different databases—from PostgreSQL to ClickHouse—using real-world query patterns."
---

Choosing the right database for analytics is hard. With many options available, each is optimized for different use cases.

Some databases are built for real-time analytics in customer-facing applications, where low-latency queries and high-ingest performance are essential. Others are designed for internal BI and reporting and optimized for large-scale aggregations and batch processing. Some databases are general-purpose, handling both transactions and analytics, while others specialize in analytical workloads.

Benchmarks can help—but only if they reflect your actual workload.

Several benchmarks, such as ClickBench, TPC-H, and TPC-DS, evaluate the performance of databases for analytics. However, they are not representative of real-time analytics.

To fill this gap, we’ve created [RTABench](https://www.rtabench.com/), a new benchmark to assist developers in evaluating the performance of different databases in real-time analytics scenarios. You can check out the benchmark tooling, datasets, and [results on GitHub](https://github.com/timescale/rtabench).

### Existing benchmarks don’t measure real-time analytics inside applications

Historically, the industry has relied on TPC-H and TPC-DS as the standard benchmarks for evaluating analytical databases. They are designed to simulate business intelligence and decision support systems that run complex, ad-hoc analytical queries across multiple tables on large data sets. This is the common use case for internal data warehouses like Snowflake or Databricks, not for real-time analytics databases.

More recently, ClickBench has emerged as a popular benchmark for analytics because it’s easy to run and contribute results. The benchmark includes public results for a comprehensive list of databases, with more than 50 across different categories (relational, NoSQL, data warehouses, real-time analytics, etc.). The results are readily available and easy to compare, making it a common reference when evaluating the analytical performance of different databases.

However, ClickBench evaluates databases using a single table of clickstream data, representative of workloads like web analytics, BI, and log aggregation. It also favors full-table large scans and large-scale aggregations on denormalized data.

Real-time analytics inside applications is different and needs a new benchmark.

## What Is Real-Time Analytics

Real-time analytics enables applications to process and query data as it is generated and as it accumulates, delivering immediate and continued insights for decision-making. It’s not about knowing what happened in the past; it’s about understanding what’s happening <em>now</em>.

Whether tracking stock prices, monitoring IoT sensor data, or analyzing user behavior, the goal is to make decisions in the moment by combining live data with historical context. These insights are often delivered through embedded dashboards or decision engines within customer-facing applications, demanding millisecond query response times.

Real-time analytics applications require low-latency ingest and queries with high concurrency to enable fast and fresh insights, efficient updates and backfills to always reflect the most accurate data, and scalability to grow with workload demands without performance degradation.

Additionally, full table scans and large aggregations on a single denormalized table do not effectively represent the query patterns in applications delivering real-time analytics.

## Real-Time Analytics Query Patterns

### 1. Queries join multiple tables

Applications store data normalized across multiple tables to ensure flexibility and efficient updates. For example, metadata and time-series/event data are stored in different tables. You need fast joins on fresh data to retrieve related records from multiple tables.

<strong>Example</strong>: <em>Show the top five assets traded by investors in the same country as the user visiting the site in the last seven days.</em>

### 2. Queries filter on specific objects and time windows

Instead of scanning everything, real-time analytics workloads filter on particular objects (e.g., users, devices, stock symbols) and recent data (e.g., last hour, last day, last week, last month). Databases built for real-time applications must excel at indexing, partitioning, and fast lookups—not just bulk aggregations over large datasets.

<strong>Example</strong>: <em>Show a stock's daily ‘candlestick’ price over the past month (vs. all stocks over the years).</em>

### 3. Pre-computed aggregations ensure instant responses

Application queries are pre-defined in application code to power specific dashboards or screens. Users expect instant insights, making pre-aggregation using incrementally updated materialized views essential.

<strong>Example</strong>: <em>Instead of computing monthly traded volume over the year for each asset on demand, an application maintains a continuously updated monthly total traded volume for each asset.</em>

Existing benchmarks like ClickBench do not benchmark pre-aggregation, but many real-time applications depend on it for sub-second response times.

### Why not just denormalize the data?

Denormalization can speed up queries—but at a cost:

- Freshness delays: ETL pipelines make real-time data stale.
- Complexity: Changing a single product name? That update might need to be written millions of times.
- Cost: More storage, more writes, more money spent.

Most real-time applications use normalized schemas and join data at query time.

## RTABench: A Benchmark for Real-Time Analytics Applications

[RTABench is a new benchmark](https://www.rtabench.com/) we have developed to evaluate databases using query patterns that mirror real-world application workloads—something missing from existing benchmarks. Unlike ClickBench and other benchmarks, RTABench closely reflects the actual needs of real-time analytics applications, measuring key factors such as joins, selective filtering, and pre-aggregations.

We want to recognize upfront that RTABench is not perfect. Evaluating performance for real-time analytics would also require testing ingest and high-concurrency queries. These additions would add a lot of complexity, make the benchmark much harder and longer to run, and introduce more variance in the results, making them harder to reproduce and interpret. We’ve decided to leave those out to make the benchmark easier to use, but we will explore ways to add them while keeping the benchmark simple to run and interpret.

## How RTABench Works

RTABench is designed to reflect real-time analytics inside applications accurately by using these elements:

### Schema: A normalized data model

[RTABench models an order tracking system with normalized tables](https://github.com/timescale/rtabench), ensuring a realistic representation of how modern applications structure data. The schema includes:

| Table Name | Description |
|---|---|
| Customers | Stores customer details, including name, location, and signup date |
| Products | Contains product catalog information, including pricing and stock levels |
| Orders | Tracks orders placed by customers |
| Order_Items | Records the products included in each order |
| Order_Events | Tracks order status changes (e.g., created, shipped, delivered) |

### Dataset: 170 million events

RTABench includes ~171 million order events, 1,102 customers, 9,255 products, and ~10 million orders. This dataset is large enough for meaningful performance testing while remaining practical for benchmarking.

### Queries: Measuring real-time performance

RTABench evaluates databases using 40 queries designed to reflect real-time application workloads. These queries test:

- <strong>Raw event queries: </strong>counting and aggregating events over time <em>(e.g., “Count the number of ‘Departed’ shipments per day at a specific terminal”)</em>
- <strong>Selective filtering: </strong>querying specific objects and time windows <em>(e.g., “Find the last recorded status of a given order”)</em>
- <strong>Multi-table joins: </strong>fetching related data across multiple tables <em>(e.g., “Show the total revenue generated by each customer in the last 30 days”) </em>
- <strong>Pre-aggregated queries:</strong> measuring performance gains from incremental materialized views <em>(e.g., “Retrieve pre-aggregated counts of delayed shipments over the last month”). </em>

By including both raw and pre-aggregated queries, RTABench ensures that databases are tested for ad-hoc analytics and optimized real-time reporting, capturing the compromises between flexibility and performance. However, because very few databases support incremental materialized views (only Timescale and ClickHouse are on the current list), we’ve moved those queries to a separate section and didn’t include the results in the overall benchmark score.

#### Built on ClickBench tooling, designed for a different use case

RTABench uses the ClickBench framework for benchmarking, but it introduces a new dataset and query set that better represents real-time analytics inside applications. All tools, datasets, and benchmark results are available on [GitHub](https://github.com/timescale/rtabench), where we welcome contributions to expand RTABench to support additional databases and optimizations.

## RTABench databases

RTABench evaluates databases built for real-time analytics inside applications, where high ingest rates, low-latency queries, and efficient joins matter most. It categorizes databases into three groups:

<strong>General-purpose databases</strong>: These are transactional databases (e.g., PostgreSQL, MySQL) that can support real-time analytics depending on scale.

<strong>Real-time analytics databases</strong>: These are optimized for high ingest, fast queries, and concurrency, often used as a secondary database.

<strong>Batch analytics databases</strong>: These are built for historical analysis and batch processing, not real-time workloads. Their results are excluded by default.

| Database | General-Purpose | Real-Time | Batch Analytics |
|---|---|---|---|
| ClickHouse |  | ✅ | ✅ |
| ClickHouse Cloud |  | ✅ | ✅ |
| DuckDB |  |  | ✅ |
| MongoDB | ✅ |  |  |
| MySQL | ✅ |  |  |
| PostgreSQL | ✅ |  |  |
| TimescaleDB | ✅ | ✅ |  |
| Timescale Cloud | ✅ | ✅ |  |

All databases are benchmarked using the same dataset and queries.

Because queries in real-time analytics applications are pre-defined and well known (vs. ad-hoc queries to a data warehouse), RTABench recommends optimizing the database configuration to achieve the best results instead of relying on the out-of-the-box setup.

## Benchmark Results: What We Learned

RTABench results are published at [<strong>rtabench.com</strong>](https://www.rtabench.com/). While performance varies based on workload characteristics, this benchmark reveals some interesting insights:

- <strong>General-purpose databases perform better on RTABench than on ClickBench. </strong>That’s expected—RTABench uses a normalized schema similar to real applications, while ClickBench is based on a denormalized dataset optimized for batch analytics.
- <strong>TimescaleDB is 1.9x faster than ClickHouse on RTABench, even though it’s 6.8x slower on ClickBench. </strong>This is likely because TimescaleDB is optimized for real-time analytics applications, which often rely on normalized schemas and selective aggregations, while ClickHouse shines in denormalized, columnar analytics with large-scale aggregations.
- <strong>Incremental materialized views offer massive speedups. </strong>They deliver up to hundreds or even thousands of times faster performance than querying the raw data (from seconds to a few milliseconds), demonstrating their value for real-time analytics. However, among the databases tested, only ClickHouse and TimescaleDB support them.
- <strong>ClickHouse is the leader in data loading and storage efficiency</strong>. It’s 4.8x faster at loading data and uses 1.7x less disk than the next best database.
- <strong>PostgreSQL was the fastest general-purpose database. </strong>The most popular database among developers demonstrates its versatility. With indexing, it’s only 4.1x slower than TimescaleDB on raw queries—but it can’t match the performance of incremental materialized views, which PostgreSQL doesn’t support.
- <strong>MongoDB struggles with normalized data. </strong>It was the slowest database in the benchmark, with six queries timing out—unsurprising given its document-based model doesn’t play well with normalized data.
- <strong>DuckDB isn’t built for real-time analytics, so it’s excluded from the main results, but it was the fastest in the benchmark. </strong>Given its popularity, we included it in the benchmark to serve as a point of reference, and it surprised us: It was 3.5x faster than TimescaleDB and 7.3x faster than ClickHouse. We didn’t expect it to beat ClickHouse, considering how well ClickHouse performs on ClickBench.

Like any benchmark, RTABench results should not be viewed as a ranking but as a guide to understanding which system aligns best with your real-time analytics needs.

## Contribute to RTABench

Not all analytics are equal. Real-time analytics inside applications is not the same as batch analytics, and the right database depends on your specific use case. RTABench provides a realistic benchmark for real-time query patterns—where multi-table joins, selective filtering, and pre-aggregations are critical. Unlike batch-oriented benchmarks focusing on full-table scans and historical aggregations, RTABench reflects how modern applications query data.

To continue improving RTABench, here’s how you can contribute:

- Adding new databases to expand the comparison
- Optimizing queries for different systems
- Providing feedback to refine configurations and ensure fairness

All benchmark tooling, datasets, and [results are available on GitHub](https://github.com/timescale/rtabench), and contributions are welcome. Explore the latest results at [rtabench.com](https://www.rtabench.com/).

