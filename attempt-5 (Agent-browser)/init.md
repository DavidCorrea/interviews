You will be in charge of reproducing an accessibility test. Your goal is to get a list of user stories that will need to be done to improve that site in terms of accessibilty for a range of different types of users.

For that, certain steps need to be followed. Those are listed below.

# Folder structure
Create the following folder structure.
- 00 - Personas
- 01 - Interviews
- 02 - Reports
- 03 - User Stories

# 00 - Personas
- For each of the scenarios listed [here](scope.md#scenarios), create a Markdown file that will describe how the persona behaves interacting with the website. Feel free to spin up a Subagent to do write up each of these personas.
- Do not take into account personas that are not present in the current folder structure.
- Each persona must have:
  - A profile
  - Behavior Rules
  - What it must do and it must not do
  - How to interact with the website
  - Instructions for a subagent to explicitly become that persona and nothing more, and also be as verbose as possible. If they need to leave the site because they're not being able to achieve their goals, they should be free to do so and explain why.

# 01 - Interviews & 02 - Reports
- For each of the personas listed in `00 - Personas`, spin up a subagent that will impersonate each persona and request them to do the listed steps in [here](scope.md#goals)
  - Instruct subagents to use `agent-browser` for web automation. They can run `agent-browser --help` for all commands.
  - For example: `agent-browser open <url>` - Navigate to page
  - Prevent taking screenshots - interact with the website. It should be used as a human would do it. We are impersonating. We need the feedback to be based on real experiences.
- The interviews must be created as a Markdown file in `01 - Interviews` and the technical details about what to improve should be put as a Markdown file in `02 - Reports`.
- Once all the reports are done, based on all of them, create a Main Report (named `_main-report.md`) in the parent folder. This file will:
  - Not have duplicate items
    - Consider grouping items if they seem related.
  - For each item:
    - Include a summary
    - Include a link of which part of the interview(s) and/or report(s) they're addressing
    - Include a priority

# 03 - User stories
Once the main report is done, please create a user story for each of the actionable items listed on the main report. These user stories should include:
- A way to test the change
- Developer notes:
  - General explanation in how it can be achieved
  - Code examples
  - Components to audit
- If possible, add examples on how other sites have achieved it.