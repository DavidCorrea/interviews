You will be in charge of reproducing an accessibility test. Your goal is to get a list of user stories that will need to be done to improve that site in terms of accessibilty for a range of different types of users.

For that, certain steps need to be followed. It is important to note that in order to perform them, no previous attempts must be taken into consideration AT ALL. The steps are:

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
- For each of the personas listed in `00 - Personas`, spin up two subagents which will run in parallel and interact between each other: an interviewer and an interviewee
  - The interviewer will request the interviewee to execute the listed steps in [here](scope.md#goals).
    - The notes about the interview, will be created in the `02 - Reports` folder as a Markdown file
      - These should only include relevant items to the interviewee and nothing else.
      - The report should describe the issues the interviewee had.
      - The interviewee might not be technical or IT-savvy at all.
      - Think of it as the outcome of the interviewer.
    - It must not execute the steps. Only the interviewee will do so.
  - The interviewee will impersonate the persona
    - It will perform the requested steps by the interviewer.
    - Create an Markdown file in `01 - Interviews` to show the experience of the persona while performing the requested steps.
    - Use `agent-browser` for web automation. Run `agent-browser --help` for all commands if needed.
      - For example: `agent-browser open <url>` - Navigate to page
      - Prevent taking screenshots - interact with the website. It should be used as a human would do it. We are impersonating. We need the feedback to be based on real experiences.
      - Do not take shortcuts.
        - Accessing a section by changing the URL is forbiden.
      - `agent-browser open` must only be called once to initially land on the website.
      - Explore the website and take actions based on your persona needs and capabilities.
- Once all the interviews are done, based on all of the reports in `02 - Reports`, create a Main Report (named `main-report.md`) in the parent folder. This file will include:
  - Summary of what the interview was about
  - A table with all the personas with their respective interviews and reports
  - All the items that came from all the different reports
    - Ensure there are not duplicate items
      - Consider grouping items if they seem related.
    - For each item:
      - Include a summary
      - Include a link of which part of the interview(s) and/or report(s) they're addressing
        - Note that you might need to update the interviews/reports to add the anchors for the links to work
      - Include a priority

# 03 - User stories
Once the main report is done, please create a user story for each of the actionable items listed on the main report. These user stories should include:
- A way to test the change once it is done to ensure the ticket has been addressed
- Developer notes:
  - General explanation in how it can be achieved
  - Code examples
  - Components to audit
- If possible, add examples on how other sites have achieved it.

# 04 - Wrapping up
Add a table in the Main Report with all the created stories sorted by priority and a link to them right after the table where the personas were listed for easy navigation. 