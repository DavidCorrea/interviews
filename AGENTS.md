# Prerequisites
- Ensure `agent-browser` is installed and usable by the interview subagents
- Ensure there is a `SCOPE.md` file in the same directory as this file (`AGENTS.md`) 
  - It must define:
    - A target Website
    - A list of goals to follow
    - A list of personas
  - It could include:
    - An outcome directory
      - If not specified, the agent will create one (see Purpose)

If any of the prerequisites is not fulfilled, do not continue with the flow and warn the user what is missing.

# What this agent and all subagents must ignore
Anything that's not this file (`AGENTS.md`), the `SCOPE.md` file or the outcome folder and its content.

# Libraries usage
## `agent-browser`
Library used for web automation. Running `agent-browser --help` will provide the available commands.

### Do's and don'ts for you and interview subagents.
#### Do
- Use `agent-browser` for open, click, type, and navigation.

#### Don't
- Do not use any other tool (MCP browser, fetch, curl, or similar) to open, load, or navigate the websites.
- Change the URL to jump to a section
- Take screenshots (except for iframes)
- Open the site more than once per session (unless they got redirected by accident)

# Purpose
You will be in charge of running an accessibility and usability test on a given website by running goal-based interviews, where each persona will try to achieve the same goals. These personas will be impersonated by subagents.
The final goal is to get a list of user stories that will need to be done to improve that site in terms of accessibility and usability.
Any output you produce must be in [the specified outcome directory](SCOPE.md#outcome-directory) in the format of Markdown files. In case it is not present, create a folder with the [website](SCOPE.md#website)'s hostname as its name.

# Interview Flow
## First step
Create the following folder structure in the outcome directory. If user asks for certain steps to be skipped, do not create the folders involving those steps.
- 00 - Personas
- 01 - Interviews
- 02 - Reports
- 03 - User Stories

## `00 - Personas` Folder
Create a file in `00 - Personas` for each of the [needed personas](SCOPE.md#personas) that will describe how the persona behaves interacting with the website. Have subagents write up each of these personas (in parallel). Instruct them to be creative. Use a consistent slug derived from the persona as the file name.

This file represents how the persona is and behaves. The persona should be plausible as someone who would try to achieve the test goals (from SCOPE); tailor background and motivation so that makes sense. All files must follow the same structure.

Each file must have:
- A very detailed identity. Must include:
  - Unique name and age
  - Tech savviness/comfort
  - Background
  - Devices it uses
- Typical mood when starting a task on a website
- Reactions to success, confusion, errors, slow load, unclear labels, and inaccessible or broken content
- Voice & Vocabulary: How they refer to UI and tasks (e.g. ‘the menu,’ ‘the sign-up thing,’ or more technical terms if it applies)
- Likes and dislikes
- Constraints or context that affect how they use the web (e.g. time pressure, assistive technology, sensory or motor needs, environment)
- Specific browsing behaviors (e.g. scans headings first, uses keyboard only, taps with thumb, reads every word, skips blocks)
- What makes them give up quickly vs. what they’ll persist through
- When the persona uses assistive technology: which tool(s), how they use it (e.g. shortcuts, verbosity), and what they expect to hear or see.
- Typical environment when using the site (e.g. at desk, on the go, in bright light, in a hurry)
- Where they expect content to be and what would surprise them (e.g. finding a section they're interested in is not present in the nav bar)

## `01 - Interviews` & `02 - Reports` Folders
Run an interview for each persona. Each persona gets a separate transcript and report.

### Transcript
Transcripts of each interview go into `01 - Interviews`. They must be produced by subagents in parallel. Use the following prompt for each of them and state explicitly that the subagent may use only `agent-browser` for web automation and no other tool:

```md
# Role
You are the persona described in `OUTCOME_DIR/00 - Personas/PERSONA_SLUG.md`. Read that file and become that persona. Act and speak only as that persona would. If a file for your persona already exists in `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`, read it and extend your context.

# Goals (attempt each one; complete them if your persona can)
- GOAL_X

# Rules
- Use only `agent-browser` for the web - no other tool. Open the site once at the start, then navigate only by using the page (links, buttons, search). Do not change the URL bar to jump to a section.
- Attempt every goal in order. If your persona cannot complete a goal, say why in the transcript and continue to the next. Do not skip a goal without trying; do not take shortcuts.
- Maintain the same session until you complete all your goals or you're not able to continue.
- Be verbose: say what you think, what you’re trying to do, what you expect, what you see or hear (e.g. if using assistive technology: what’s announced, what’s focusable, what’s confusing or missing).
- Do not infer or assume anything about the site; only report what you actually do and experience. Do not use technical jargon unless your persona would.

# Deliverable
When you finish, save your first-person transcript to this exact path: `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. The transcript must be the full experience of the persona (what you did, saw, found hard, where you got stuck). You may add a short summary at the end, but the body must be the step-by-step experience. This file is your required deliverable.
```

Replace:
- `OUTCOME_DIR` for the absolute path to the outcome directory
- `PERSONA_SLUG` for the persona slug that this subagent will impersonate
- `GOAL_X` for the [list of goals](SCOPE.md#goals) that must be achieved.

When you invoke each interview subagent, capture and store the agent ID returned when that subagent’s task completes, and associate it with the persona slug and the name they were given.

### Report
Once all interviews are done, create a report based on each interview (using the same persona slug as the transcript) and save it in `02 - Reports`.
They must include:
- The persona that was interviewed
- A summary including the goals completion
- A list of all the issues that the interviewer noticed in the interview
  - These must include a link to the part where the issue is found in the transcript
- A section of what worked well

## Follow-up questions
Create a file named `follow-up.md` in the outcome directory. 

It must contain:
- A short sentence explaining that the user can use the agent IDs in the table below to resume the corresponding persona subagent later (e.g. via the platform’s resume feature) to ask further questions.
- A table with three columns: **Persona** (persona slug), **Name** (the name they were given) and **Agent ID**. Populate one row per interview subagent with the agent ID that was returned when you invoked that subagent. If an agent ID was not returned or could not be captured for a persona, leave the Agent ID cell empty or note "not available".

The user may ask you to ask more questions to a specific persona. They might refer to either the persona slug or the name they were given. If so:
- Use the table to find the Agent ID for the requested persona and resume that subagent with the user’s question by using the following prompt:
```md
# Role
You are still the persona described in `OUTCOME_DIR/00 - Personas/PERSONA_SLUG.md`. You already completed your interview; your transcript is in `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Stay in character and impersonate that persona: act, think, and speak only as they would.

# Follow-up question
The user is asking: USER_QUESTION

# Task
Respond only as that person would, in first person, in their voice - not as an assistant describing the persona. If you need to check the website to answer accurately, use only `agent-browser` (open the site once, then navigate only via the page—no URL bar). If you can answer from your experience in the transcript, do that.

# Deliverable
Append your response to `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Add a clear section (e.g. "## Follow-up" or "### Follow-up") with the user's question and your answer, so the transcript stays one continuous story.
```
- When invoking, replace `OUTCOME_DIR`, `PERSONA_SLUG`, and `USER_QUESTION` in the prompt.
- If the answer reveals new issues or observations, update that persona’s report (add issues with links to the new transcript section, update “what worked well” if relevant)
- If there are new findings that belong in the main report, add them to Main Report (summary, link, priority) and deduplicate/group with existing items.
- Add a new section after the "Personas, Interviews, and reports" section named "Follow up questions" where, in a table, is listed who it was requested a follow-up, when, the new goal and a link to the follow up in the transcript. If the section already exists, just add a new row.

### Fallback
If the question cannot be done to the persona (either because the subagent ID is not valid or the subagent could not be found), start a new subagent and use the following prompt:
```md
# Role
You are the persona described in `OUTCOME_DIR/00 - Personas/PERSONA_SLUG.md`. An interview transcript for this persona already exists at `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Read that file to get context on what you did and experienced during the interview. Impersonate that persona: Act and speak only as they would.

# Follow-up question
The user is asking: USER_QUESTION

# Task
Stay in character and answer as the persona would, in first person. If the question requires checking the website, use only `agent-browser` (open the site once, then navigate only via the page—no URL bar). Otherwise answer from the transcript and your persona. Do not redo the full interview; only address this follow-up.

# Deliverable
Append your response to `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Add a clear section (e.g. "## Follow-up" or "### Follow-up") before the summary (if exists) with the new goal and your answer.
```
When invoking, replace `OUTCOME_DIR`, `PERSONA_SLUG`, and `USER_QUESTION` in the prompt.

## Main Report
Once all the interviews are done, based on all of the reports, create a Main Report (named `main-report.md`) in the outcome directory. This file will include:
  - Summary of what the interview was about
  - A table with the goals listed
  - A table with all the personas and their names with their respective interviews and reports
  - A table with created user stories (if any)
  - A table with the follow-up questions
  - All the items that came from all the different reports
    - Ensure there are no duplicate items
      - Consider grouping items if they seem related.
    - For each item:
      - Include a summary
      - Include a link of which part of the interview(s) and/or report(s) they're addressing
      - Include a priority

## User Stories Folder
Once the main report is done, please create a user story for each of the actionable items listed on the main report. These user stories should include:
- Acceptance criteria
- Examples on how other sites have achieved it (Optional)

## Wrapping up
Add a table in the Main Report with all the created stories sorted by priority (Critical, High, Medium and Low) and a link to them right after the table where the personas were listed for easy navigation. 
