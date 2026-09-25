---
title: "Agent-A-Thon Final Day: AI Agents Planning, Coding and Testing Together"
---

Last night, at around 1 AM, I submitted my Agent-A-Thon presentation.

To prepare the demo, I had to put the system to real work and see how well it performed. Yesterday afternoon I was keeping my fingers crossed that everything would work as intended. It did, although not without a few surprises along the way. Fortunately, those challenges became excellent learning opportunities.

I challenged my agentic team with the following GitHub issue:

**Title:** Add employee search by name

**Description:**
> On Employee table view, add a text box where user can type a name, label it "Surname". Beside it add a Search button. The controls should be placed above the employee list. When a user enters a name and clicks Search, employees whose names contain the search term should be displayed. If the search value is `*` or empty, all employees should be shown.


## Planning the Change

The process started with the Planning Agent, which was responsible for selecting the files that needed to be modified.

On the first run, the agent hallucinated and suggested files that did not exist in the repository. That caused the workflow to fail later in the process. After improving the prompt and tightening the instructions, the agent was able to identify the correct files and the process moved forward.

## Implementation Agent at Work

Next, I handed the selected files to the Implementation Agent.

The agent analyzed the issue, modified the code, created a pull request, and proposed the implementation. After reviewing the changes, I approved the PR and merged it.

The deployment to Azure completed successfully, but during testing I noticed that the search controls had been added twice. The page contained duplicate input fields and Search buttons. I had deliberately chosen to validate the feature in the deployed application rather than focus only on the code review. The duplication could probably have been detected earlier during review, but verifying the deployed result helped validate the end-to-end workflow.

Removing the extra controls was a quick fix and the feature then worked as expected.

For this experiment I used gpt-5.4-mini as the implementation model. Stronger coding models would likely make fewer mistakes, but overall I was impressed by how much useful work the agent produced.

## Automated Test Generation

After the implementation had been merged, the Test Automation Agent took over.

Its responsibility was to analyze the change and generate a Playwright test automatically.

Getting the workflow running required several iterations. Most of the work was actually related to improving the GitHub Actions workflow and making sure all required context reached the agent correctly.

Eventually the Test Agent generated a Playwright test and I executed it in a separate workflow.

The generated test needed a few fixes:
- Added one missing navigation step
- Corrected how employee names were selected from the table

These were ordinary test updates rather than major rewrites.
Late in the evening the test finally passed successfully.

## Creating the Demo

The final stretch was creating the demonstration video and presentation video for the submission. Producing and editing the recordings took several hours.

I deliberately chose not to leave the finishing touches for the morning and completed everything during the night. Seeing the entire flow work end-to-end made the effort worthwhile. Here is the demo run

<video controls width="420">
    <source src="./images/2026-09-24-frontierweek.mp4" type="video/quicktime" />
    Your browser does not support the video tag.
</video>

## What I Learned

The most valuable outcome was realizing that I now had an AI-assisted team supporting me across the entire development lifecycle:
- Planning
- Implementation
- Testing

The agents were not perfect, but they produced remarkably useful analysis, code changes, pull requests, and test automation.

Another benefit was the process itself. Because everything happened through GitHub Issues, Pull Requests, and GitHub Actions, the workflow remained highly structured and transparent. It was easy to trace the decisions made by each agent and understand how the final result was produced.

In the end, the agents did most of the heavy lifting while I focused on review, corrections, and quality control.

If you'd like to explore the code, you can find the project repository here:
[palapiessa/hrApp](https://github.com/palapiessa/hrApp)

It was great fun to work on the project and well worth the effort, regardless of the final competition results. I am also grateful for the opportunity to participate in the event and learn from other talented builders and their ideas.  The winners will be announced on October 2nd, and I'm looking forward to seeing all the impressive solutions that were created during the event.

#AI #AgenticAI #AzureAI #AzureAIFoundry #GitHubActions #Playwright #SoftwareTesting #DevOps #Automation #QualityEngineering #Hackathon