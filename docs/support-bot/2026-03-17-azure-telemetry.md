---
title: "Part 4: QA telemetry"
---
<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
<script>mermaid.initialize({ startOnLoad: true });</script>

In previous chapter the support bot was evaluated with several factors. The first test run can be used as a baseline to compare future test runs with. If this bot should end up in production it would require further development resulting in multiple test runs. Then 
a centralized result store would help to keep results organized. It would also enable a searchable timeline and provide query tools to analyze results and create trend analysis. A team or stakeholders would be kept informed about the quality of the app with a common dashboard. It is also vital to have decent logging and monitoring in place when AI is incorporated in development process.

There are multiple platforms such data can be stored into. For this blog I chose *Azure* which is widely used. *Weights and Biases* is another suitable cloud based pltaform, and it requires less setup work than Azure. Results can also be sent to an internal platform such as for example *Sharepoint*. 

## Steps to send results to Azure
In Azure the results are stored in Application Insights instance. One needs to be created for this purpose. Also a Log Analytics Workspace is required. 

The Azure monitor SDK is used in `run_grader.py` to send the results into Application Insights. An evironment variable `APPLICATIONINSIGHTS_CONNECTION_STRING` needs to be loaded into memory before connection can work. Then an Azure logger can be created in Python:
```python
import logging
from azure.monitor.opentelemetry import configure_azure_monitor

load_dotenv(find_dotenv())
configure_azure_monitor(logger_name="grader")
logger = logging.getLogger("grader")
logger.setLevel(logging.INFO) 
```

When logger is instantiated it can be called for example like this:
```python
logger.info(
		"Row graded",
		extra={
			"question": question[:100],
			"passed": str(score.passed),
			"semantic_correctness": score.semantic_correctness,
			"helpfulness": score.helpfulness,
			"tone_safety": score.tone_safety,
		},
	)
```
See the source code for logger calls. Run the grader from project root to see results flow to Azure:

```bash
$ PYTHONPATH=./support_bot/src ./.venv/bin/python ./grader/src/run_grader.py --answers-csv ./grader/data/llm_eval_answers.csv --output-jsonl ./grader/data/llm_eval_scores.sample.jsonl
````






## Disclaimer
This post and sample code are for educational purposes.
They are provided "as is" without warranties, and you should validate suitability, safety, and security before production use.
