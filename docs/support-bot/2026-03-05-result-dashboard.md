---
title: "Part 4: QA telemetry in Azure"
---
<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
<script>mermaid.initialize({ startOnLoad: true });</script>

In previous chapter the support bot was evaluated with several factors. And the resulting values are suitable for analysing the variation between test runs, the *deltas*. This data is interesting for both the developers and other stakeholders. Data is required to prove the quality of the product is improving and not decreasing.

There are multiple platforms such data can be stored into. For this blog I chose *Azure* which is widely used. *Weights and Biases* is another suitable option, it requires less setup work than Azure. Monitor can also send alerts for declining values.  

## Disclaimer
This post and sample code are for educational purposes.
They are provided "as is" without warranties, and you should validate suitability, safety, and security before production use.
