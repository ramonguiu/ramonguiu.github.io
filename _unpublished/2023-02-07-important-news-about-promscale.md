---
title: "Important News About Promscale"
date: 2023-02-07
publication: Tiger Data blog
original_url: https://www.tigerdata.com/blog/important-news-about-promscale
canonical_url: https://www.tigerdata.com/blog/important-news-about-promscale
archive_url: https://web.archive.org/web/20260810012922/https://www.tigerdata.com/blog/important-news-about-promscale
description: "We regret to inform you that we’ve made the difficult decision to discontinue Promscale. In this blog post, we answer your FAQs and offer alternatives."
---

Dear community,

<strong><em>We regret to inform you that we’ve made the difficult decision to discontinue Promscale, our unified metric and trace observability backend for Prometheus, Jaeger, and OpenTelemetry built on PostgreSQL and TimescaleDB.</em></strong>

### If you were sent to this page while looking for more Promscale information

You have a list of all the Promscale GitHub repositories below (we stopped maintaining or evolving them on April 30, 2023), as well as alternatives and frequently asked questions.

### If you'd like to learn more about Prometheus, Jaeger, or OpenTelemetry

 You will find several resources in our blog:

- [A Deep Dive Into the Four Types of Prometheus Metrics](https://www.tigerdata.com/blog/four-types-prometheus-metrics-to-collect/)
- [A Deep Dive Into OpenTelemetry Metrics](https://www.tigerdata.com/blog/a-deep-dive-into-open-telemetry-metrics/)
- [Prometheus vs. OpenTelemetry Metrics: A Complete Guide](https://www.tigerdata.com/blog/prometheus-vs-opentelemetry-metrics-a-complete-guide/)
- [How Prometheus Querying Works (and Why You Should Care)](https://www.tigerdata.com/blog/how-prometheus-querying-works-and-why-you-should-care/)
- [“How to Analyze Your Prometheus Data in SQL” Recap and Resources](https://www.tigerdata.com/blog/how-to-analyze-your-prometheus-data-in-sql-recap-and-resources/)

### But wait, what is Timescale?

Timescale is a mature cloud database built on PostgreSQL. It supercharges PostgreSQL, giving it the boost it needs to handle large volumes of metrics, [keeping your writes and queries fast](https://www.tigerdata.com/blog/postgresql-timescaledb-1000x-faster-queries-90-data-compression-and-much-more/) via [automatic partitioning](https://www.timescale.com/learn/is-postgres-partitioning-really-that-hard-introducing-hypertables?ref=timescale.com), query planner enhancements, improved materialized views, [columnar compression](https://www.tigerdata.com/blog/building-columnar-compression-in-a-row-oriented-database), and much more.

[Check the Timescale Docs to learn more](https://docs.timescale.com/).

### If you want to learn more about why we deprecated Promscale

Keep reading.

### Important News About Promscale

Promscale was created to help the community use PostgreSQL/TimescaleDB as a fully compliant remote storage for Prometheus. Later on, we added OpenTelemetry and [Jaeger tracing](https://www.tigerdata.com/blog/what-is-distributed-tracing-and-how-jaeger-tracing-is-solving-its-challenges) support.

With its full SQL support, it provided unified storage for traces and metrics with deep analysis and correlation capabilities. We also built tobs to simplify the deployment of a complete observability stack with one command.

Promscale has been a labor of love for our team at Timescale for over two years, and we’re grateful for the support and feedback from you, our community of users. However, after reevaluating our company priorities, we’ve decided to redirect our resources to other product areas.

We understand this news may be disappointing, so please see the FAQ for answers to common questions, including alternative solutions.

Thanks again for your support.

##
FAQs

### Why is Promscale discontinued?

We’re refocusing all our efforts on the core of what we do best, creating a great developer experience for time-series application developers.

### What happens next?

The following GitHub repositories and documentation will remain publicly available but will no longer be evolved nor maintained:

- [https://github.com/timescale/promscale](https://github.com/timescale/promscale)
- [https://github.com/timescale/promscale_extension](https://github.com/timescale/promscale_extension)
- [https://github.com/timescale/tobs](https://github.com/timescale/tobs)
- [https://github.com/timescale/helm-charts/tree/main/charts/promscale](https://github.com/timescale/helm-charts/tree/main/charts/promscale)
- [https://promscale-legacy-docs.timescale.com/](https://promscale-legacy-docs.timescale.com/)

### Can I keep using Promscale with TimescaleDB?

You can continue to use Promscale with TimescaleDB, although we don’t recommend it since Promscale will no longer be supported or maintained.
The GitHub repositories and release artifacts will remain publicly available.

We can’t ensure that Promscale will continue to work with newer versions of TimescaleDB and PostgreSQL. If you want to make modifications, we encourage you to fork the repositories.

### Who do I contact if I am a customer of Timescale and I need critical support?

Contact the support team at [support@timescale.com](mailto:support@timescale.com) or [https://www.timescale.com/support](https://www.timescale.com/support).

### What Promscale alternatives do you recommend?

There are different options depending on your use case. <strong>If you use Promscale as remote storage for Prometheus</strong>, there are a number of other options you can consider. There is a list provided in the [Prometheus documentation](https://prometheus.io/docs/operating/integrations/#remote-endpoints-and-storage).

<strong>If you are using Promscale as a storage system for your OpenTelemetry or Jaeger traces,</strong> there are a number of options you can consider.

[This is a list of products that have native support for OpenTelemetry](https://opentelemetry.io/ecosystem/vendors/). You can use the OpenTelemetry Collector to convert your OpenTelemetry traces to Jager traces.

If you have a specific need, you can ask in the #promscale channel in [Timescale's Community Slack](https://slack.timescale.com/), and we’ll try to help you.

