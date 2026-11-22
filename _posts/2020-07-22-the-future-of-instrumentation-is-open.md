---
title: "The Future of Instrumentation Is Open: Introducing Open Source Agents and Projects at New Relic"
date: 2020-07-22
publication: New Relic blog
original_url: https://newrelic.com/blog/dem/introducing-open-source-agents-and-projects
archive_url: https://web.archive.org/web/20260124181851/https://newrelic.com/blog/dem/introducing-open-source-agents-and-projects
description: New Relic open-sources its agents, integrations and SDKs and standardizes on OpenTelemetry.
---

At New Relic, we want to enable every engineer to gather complete telemetry from their software and systems. Since our founding in 2008, we’ve invested hundreds of thousands of engineering hours developing instrumentation, including comprehensive support for multi-language application framework instrumentation. Over the last year, we’ve also been a [top contributor](https://opentelemetry.devstats.cncf.io/d/5/companies-table?orgId=1&var-period_name=Last%20month&var-metric=contributions) to the Cloud Native Computing Foundation’s OpenTelemetry project, and we believe the future of instrumentation is open.

In that spirit, today we’re excited to announce that we are making our agents, integrations, and SDKs available under an open source license. We believe our open source instrumentation will provide you with complete transparency about the code you deploy to your systems, and that by taking an open source approach, we can better engage with you on feedback and increase the pace of innovation and quality of our product.

### We’re open sourcing our instrumentation

Starting today, our agents for [C](https://github.com/newrelic/c-sdk), [Go](https://github.com/newrelic/go-agent), [.NET](https://github.com/newrelic/newrelic-dotnet-agent), [Node](https://github.com/newrelic/node-newrelic), [Python](https://github.com/newrelic/newrelic-python-agent), and [Ruby](https://github.com/newrelic/newrelic-ruby-agent), as well as the [Infrastructure agent](https://github.com/newrelic/infrastructure-agent), [Infrastructure integrations](https://docs.newrelic.com/docs/integrations/infrastructure-integrations/get-started/introduction-infrastructure-integrations#on-host-integrations), the [Infrastructure Integrations SDK](https://docs.newrelic.com/docs/infrastructure/host-integrations/infrastructure-integrations-sdk/get-started/introduction-infrastructure-integrations-sdk/), and [Telemetry SDKs](https://docs.newrelic.com/docs/data-ingest-apis/get-data-new-relic/new-relic-sdks/telemetry-sdks-send-custom-telemetry-data-new-relic) are available and open to contributions in New Relic’s [GitHub organization](https://github.com/newrelic). The remaining agents will be available soon—Java in September, PHP in October, and Browser and Mobile in 2021.

Our commitment to open source instrumentation goes beyond sharing our source code. We’ll also publish roadmaps for our open source products in each repo. Additionally, you’ll be able to report issues and make feature requests for those products directly on GitHub. These changes will give you a familiar channel for accessing New Relic expertise and product information and for collaboration and feedback.

*Bestow is focused on delivering amazing experiences for our customers, and New Relic is an important partner to provide us observability,* said **Chris Bartels, Engineering Manager at [Bestow](https://bestow.com/)**. *To be able to jump in and contribute to their open source projects and get help from their team will be hugely helpful for my team and show that we have a great partnership with New Relic.*

### We’re a top contributor to—and are standardizing on—OpenTelemetry

We’re encouraged by the broad and growing acceptance of [OpenTelemetry](https://opentelemetry.io/)—a [Cloud Native Computing Foundation](https://www.cncf.io/) project—as the emerging standard for software instrumentation. Achieving ubiquitous instrumentation across all existing and emerging software technologies is an effort best served by collaboration among the community and the adoption of a reduced set of standards to align our efforts. Because of that, we’re standardizing our future observability offerings on OpenTelemetry, increasing our investments in the project to become a major contributor to this standard, and evolving our strategy to fully embrace open instrumentation.

We're a top contributor to the OpenTelemetry SDKs for Java, Go, and C/C++ and today’s announcement only deepens that engagement.

We’ll contribute our instrumentation to OpenTelemetry projects, including support for the hundreds of frameworks and libraries that provide you unparalleled breadth of visibility. We’ve also taken a leadership role in OpenTelemetry metrics, contributing twelve years’ worth of experience to the metrics semantic specification, as we believe metrics are fundamental to understanding, monitoring, and observing the health and performance of a service.

If you are experimenting with the beta version of OpenTelemetry, you can use our exporters for [Java](https://github.com/newrelic/opentelemetry-exporter-java), [Go](https://github.com/newrelic/opentelemetry-exporter-go), and the [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/master/exporter/newrelicexporter) to send telemetry from your services to New Relic, as demonstrated [in this tutorial](https://blog.newrelic.com/engineering/getting-started-with-opentelemetry-for-java-and-new-relic/). A new UI provides an out-of-the-box experience to easily surface and troubleshoot application errors and visualize distributed traces to identify bottlenecks and anomalous behaviors.

To help you easily adopt OpenTelemetry, we’ll provide an OpenTelemetry agent that will include the OpenTelemetry SDK, OpenTelemetry auto-instrumentation (where available), and our [OpenTelemetry exporter](https://docs.newrelic.com/docs/integrations/open-source-telemetry-integrations/open-source-telemetry-integration-list/new-relics-opentelemetry-integration). Our agent will provide the features and functionality that you expect from a complete application service observability solution, while enabling real-time metrics visualization, expanded filtering and faceting of metrics, and a growing ecosystem of open instrumentation.

The OpenTelemetry agent—an open source downstream extension of OpenTelemetry—will include compatibility with most features of our original agents to ease the update process. Going forward, we’ll contribute instrumentation and its features to the OpenTelemetry project, so you benefit regardless of what observability backend you use. We’ll deliver production-ready OpenTelemetry agents for all programming languages we support by summer 2021.

**Don’t miss:** [OpenTelemetry: Future-Proofing Your Instrumentation](https://blog.newrelic.com/product-news/what-is-opentelemetry/)

### We’re ready for the future of open instrumentation

We believe in open instrumentation. By contributing our hard-earned expertise in creating visibility to myriad languages, frameworks, datastores, and other systems, we’re making it easier for you to enable observability best practices in your systems. These are bold steps we’re taking today, but they’re only the beginning. We know what a dedicated group of engineers working in close and open collaboration can achieve, and we can’t wait to play our part in this journey.

**Visit [New Relic Open Source](https://opensource.newrelic.com) to learn more about our open source projects and contributions.**

<div class="meta" markdown="1">

*This post contains “forward-looking” statements, as that term is defined under the federal securities laws, including but not limited to statements regarding the timing and benefits of our open source offerings and contributions to OpenTelemetry, including the future availability of agents, potential open source roadmaps, and other additional features and functionalities. The achievement or success of the matters covered by such forward-looking statements are based on New Relic’s current assumptions, expectations, and beliefs and are subject to substantial risks, uncertainties, assumptions, and changes in circumstances that may cause New Relic’s actual results, performance, or achievements to differ materially from those expressed or implied in any forward-looking statement. Further information on factors that could affect New Relic’s financial and other results and the forward-looking statements in this post is included in the filings New Relic makes with the SEC from time to time, including in New Relic’s most recent Form 10-K, particularly under the captions “Risk Factors” and “Management’s Discussion and Analysis of Financial Condition and Results of Operations.” Copies of these documents may be obtained by visiting New Relic’s Investor Relations website at http://ir.newrelic.com or the SEC’s website at www.sec.gov. New Relic assumes no obligation and does not intend to update these forward-looking statements, except as required by law.*

</div>
