# Project Information
## Prerequisites
- Ensure `agent-browser` is installed and usable by the interview subagents
- Ensure there is a `SCOPE.md` file in the same directory as this file (`AGENTS.md`) 
  - It must define:
    - A target Website
    - A list of goals to follow
    - A list of personas
  - It could include:
    - An outcome directory

If any of the prerequisites is not fulfilled, do not continue with the flow and warn the user what is missing.

# Your purpose
You will be in charge of running an accessibility and usability test on a given website by running goal-based interviews, where each persona will try to achieve the same goals. These personas will be impersonated by subagents. The persona subagent is a real user on a live site: they look at the page and report what they see.

The final goal is to get a list of user stories that will need to be done to improve that site in terms of accessibility and usability.

## Outcome directory
Any output you produce must be in a folder with the [website](SCOPE.md#website)'s hostname as its name. If an outcome directory is defined in [the scope](SCOPE.md), use the specified folder in that section instead.

# Interviews Flow
## First step
Create the following folder structure in the outcome directory. 

Note: The user might ask for certain steps to be skipped, do not create the folders involving those steps.

- [`00 - Personas`](#00---personas-folder)
- [`01 - Interviews`](#01---interviews--02---reports-folders)
- [`02 - Reports`](#01---interviews--02---reports-folders)
- [`03 - User Stories`](#03---user-stories-folder)

## `00 - Personas` Folder
Create a file in `00 - Personas` for each of the [needed personas](SCOPE.md#personas) that will describe how the persona behaves interacting with the website. Use a consistent slug derived from the persona as the file name.

Have subagents write up each of these personas (in parallel).

Instruct these subagents to be creative: This file represents how the persona is and behaves. The persona should be plausible as someone who might use this kind of website. Describe how they behave on the web in general; do not over-tailor the persona to the exact test goals (avoid naming specific topics, tasks, or labels from the goals).

All files must follow the same structure:
- A very detailed identity, including:
  - Name and age
  - Tech savviness/comfort
  - Background
  - Devices it uses
- Typical mood when starting a task on a website
- Reactions to success, confusion, errors, slow load, unclear labels, and inaccessible or broken content
- Voice & Vocabulary: How they refer to UI and tasks (e.g. ‘the menu,’ ‘the sign-up thing,’ or more technical terms if it applies)
- Likes and dislikes: Everyone has a preference on what they want or don't want on a site. It might lead to make them come back again or not
- Constraints or context that affect how they use the web (e.g. time pressure, assistive technology, sensory or motor needs, environment)
- Specific browsing behaviors (e.g. scans headings first, uses keyboard only, taps with thumb, reads every word, skips blocks)
- How they typically read/scan the page (e.g. from the top and left-to-right). This will be based on how the persona would do it.
  - People who read in other languages (e.g. right-to-left) or who use assistive technology (e.g. screen readers, keyboard navigation) may experience the page in a different order; the subagent must respect the persona's described behavior and follow how that persona would actually read or navigate (as described in the persona file) instead of the default top-to-bottom order when it applies.
- What makes them give up quickly vs. what they’ll persist through
- When the persona uses assistive technology: which tool(s), how they use it (e.g. shortcuts, verbosity), and what they expect to hear or see.
- Typical environment when using the site (e.g. at desk, on the go, in bright light, in a hurry)
- Where they expect content to be and what would surprise them (e.g. finding a section they're interested in is not present in the nav bar)
- Do not mention the specific test goals or goal-related topics unless they are a natural part of the character's backstory. Background can reference why they might use this site (e.g. industry or role), but describe behavior (scan order, reactions, expectations) in general terms so the persona works for any set of goals on the site.

After all the personas are created, ensure they all have unique names. This will help for the follow-up questions to know who the question is for.

## `01 - Interviews` & `02 - Reports` Folders
Run an interview for each persona. Each persona gets a separate transcript and report.

### Transcript
Transcripts of each interview go into `01 - Interviews`. They must be produced by subagents in parallel. Use the following prompt for each of them:

```md
{{SETUP}}

# Role
You are the persona described in `OUTCOME_DIR/00 - Personas/PERSONA_SLUG.md`. Read that file and become that persona. Act and speak only as that persona would. If a file for your persona already exists in `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`, impersonate that persona.

# Goals (attempt each one as your persona would; complete them if your persona can)
- GOAL_X

# Rules
- Attempt every goal in order. If your persona cannot complete a goal, say why in the transcript and continue to the next.
{{RULES_LIST}}

# Deliverable
When you finish, save your first-person transcript to this exact path: `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. The transcript must be the full experience of the persona (what you did, saw, found hard, where you got stuck). Add a summary at the end. It must include:
- What you would change (i.e. issues you had)
- What you would keep
- What you would improve
- If you were able to reach your goals

This file is your required deliverable.
```

Replace in order:
- `{{SETUP}}` with the full [Setup](#setup) section.
- `{{RULES_LIST}}` with the full [Rules](#rules) section.
- `OUTCOME_DIR` for the absolute path to the outcome directory
- `PERSONA_SLUG` for the persona slug that this subagent will impersonate
- `GOAL_X` for the [list of goals](SCOPE.md#goals) that must be achieved.

When you invoke each interview subagent, capture and store the agent ID returned when that subagent’s task completes, and associate it with the persona slug and the name they were given.

Once all transcripts are created, delete the `.tmp` folder inside `01 - Interviews` (if present).

### Report
Once all interviews are done, create a report based on each interview (using the same persona slug as the transcript) and save it in `02 - Reports`.
All reports must follow the same structure:
- Interviewee: The persona that was interviewed, including a link to its interview
- Summary: A summary including the goals completion
- Encountered issues: A list of all the issues that were identified in the interview
  - These must include a link to the part where the issue is found in the transcript
- What worked well: A list of all the things that were positive from the interviewee's point of view

## Main Report
Once all the interviews are done, based on all of the reports, create a Main Report (named `main-report.md`) in the outcome directory. This file will include the following sections:
  - Summary: Summary of what the interviews were about including when they happened
  - Interviewees: A table with all the personas and their names with links to their respective interviews and reports
  - Goals: A list of all the goals that were requested to all the personas
  - Follow-up questions: A table with the follow-up questions, including:
    - Who it was made to
    - When
    - A link to their response in the transcript
  - Outcome: All the items that came from all the different reports
    - Ensure there are no duplicate items
      - Consider grouping items if they seem related.
    - Each item must have:
      - A summary
      - A link of which part of the interview(s) and/or report(s) they're addressing
      - A priority
  - User stories: A table with the created user stories sorted by priority (Critical, High, Medium and Low)
    - If none was created, avoid creating this section

## `03 - User Stories` Folder
Once the main report is done, please create a user story for each of the actionable items listed on the main report. These user stories must include:
- Acceptance criteria
- Examples on how other sites have achieved it

## Follow-up questions
After all interviews are done, create a file named `follow-up.md` in the outcome directory and populate the table with one row per interview subagent (persona slug, name, agent ID from what you captured during the flow).

It must contain a table with three columns:
- Persona (the persona slug),
- Name (the name they were given)
- Agent ID

If an agent ID was not returned or could not be captured for a persona, leave the Agent ID cell empty.

The user may ask you to ask more questions to a specific persona. They might refer to either the persona slug or the name they were given. If so:
- If the user's question is about what is on the site or whether the persona saw something, include in the prompt you send: "You must open the site with agent-browser and look at the page before answering. Do not answer from the transcript."
- Use the table to find the Agent ID for the requested persona and resume that subagent with the user’s question by using the following prompt:
```md
{{SETUP}}

# Role
You are still the persona described in `OUTCOME_DIR/00 - Personas/PERSONA_SLUG.md`. You already completed your interview; your transcript is in `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Stay in character and impersonate that persona: act, think, and speak only as they would.

# Follow-up question (answer it as your persona would; complete it if your persona can)
The user is asking: USER_QUESTION

# Rules
- Do not answer from the transcript or from memory. Visit the site again to do what you need to do.
- Only for purely retrospective questions (e.g. how you felt, what you thought at the time) may you answer from the transcript alone.
{{RULES_LIST}}

{{FOLLOW_UP_DELIVERABLE_SECTION}}
```

Replace in order:
- `{{SETUP}}` with the full [Setup](#setup) section.
- `{{RULES_LIST}}` with the full [Rules](#rules) section.
- `{{FOLLOW_UP_DELIVERABLE_SECTION}}` with the full [Follow-up deliverable](#follow-up-deliverable) section.
- `OUTCOME_DIR` for the absolute path to the outcome directory
- `PERSONA_SLUG` for the persona slug that this subagent will impersonate
- `USER_QUESTION` for the question the user asked to this persona.

### Fallback
If the question cannot be done to the persona (either because the subagent ID is not valid or the subagent could not be found), start a new subagent and use the following prompt:
```md
{{SETUP}}

# Role
You are the persona described in `OUTCOME_DIR/00 - Personas/PERSONA_SLUG.md`. An interview transcript for this persona already exists at `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Read that file to get context on what you did and experienced during the interview. Impersonate that persona: Act and speak only as they would.

# Follow-up question (answer it as your persona would; complete it if your persona can)
The user is asking: USER_QUESTION

# Rules
- Do not answer from the transcript or from memory. Visit the site again to do what you need to do.
- Only for purely retrospective questions (e.g. how you felt, what you thought at the time) may you answer from the transcript alone.
{{RULES_LIST}}

{{FOLLOW_UP_DELIVERABLE_SECTION}}
```

Replace in order:
- `{{SETUP}}` with the full [Setup](#setup) section.
- `{{RULES_LIST}}` with the full [Rules](#rules) section.
- `{{FOLLOW_UP_DELIVERABLE_SECTION}}` with the full [Follow-up deliverable](#follow-up-deliverable) section.
- `OUTCOME_DIR` for the absolute path to the outcome directory
- `PERSONA_SLUG` for the persona slug that this subagent will impersonate
- `USER_QUESTION` for the question the user asked to this persona.

### New issues or observations
The answer might reveal new issues or observations. If so update that persona’s report:
  - Add issues with links to the new transcript section
  - Update “what worked well” if relevant

### Main Report updates
- If there are new findings, add them (summary, link, priority) and deduplicate/group with existing items
- Update the "Follow up questions" section

## Subagent prompts
### Setup
When you build any prompt for an interview subagent (interview, follow-up, or fallback), replace `{{SETUP}}` in that prompt with the following block to the prompt:
```md
# Initial setup
- **Never run `cd`.** Do not change directory for any reason. Run every command from the workspace root. Stay in the same directory for the entire task. (Wrong: `cd OUTCOME_DIR` or `cd /some/path`. Right: pass the full path as an argument, e.g. `mkdir "/full/path/to/folder"` or write to `/full/path/to/file.md`.)
- Use absolute paths for any path you use: reading or writing files, creating or deleting folders, saving screenshots, and any other file or directory operation. OUTCOME_DIR in this prompt is replaced with the absolute outcome path; use that value (or the full path) for all such operations — do not cd into it and do not use relative paths.
- Before starting, read the `agent-browser` skill at `.agents/skills/agent-browser/SKILL.md` and the references in `.agents/skills/agent-browser/references/` so you know all commands and patterns.
```
When inserting this block, remember to replace OUTCOME_DIR with the same absolute path used elsewhere in the prompt.

### Rules
When you build any prompt for an interview subagent (interview, follow-up, or fallback), replace `{{RULES_LIST}}` in that prompt with the following block to the prompt:

```md
- All interactions with the website must follow how your persona would do it.
- Be explicit and very verbose: say what you think, what you’re trying to do, what you expect, what you see or hear (e.g. if using assistive technology: what’s announced, what’s focusable, what’s confusing or missing). Do not spare any detail or take anything for granted.
- Adjust the browser (e.g. device, viewport, dark or light mode, etc.) to how your persona would use it.
- Report all the interactions you have with the website.
- Use any taken screenshots in `OUTCOME_DIR/01 - Interviews/.tmp/PERSONA_SLUG` to have even more context on what is happening and how it would affect your experience and achieving what you need to do.
- Do not skip without trying and do not take shortcuts (e.g. trying to access a section by manually typing the URL).
- Maintain the same session until you finish or you're not able to continue.
- Do not infer or assume anything about the site; only report what you actually do and experience. Do not use technical jargon unless your persona would.

## Regarding `agent-browser` usage
- **Do not run `cd`.** Keep your shell in the workspace root; use absolute paths for all file and folder operations.
- It is the only tool to navigate the web - no other tool. Open the site (i.e. calling `open`) once at the start, then navigate only by using the page (e.g. links, buttons, search). Do not change the URL bar to jump to a section.
- Do not describe the page from assumption or from a prior run.
- Taking and using screenshots feature take precedence over snapshots
  - Do NOT annotate the screenshot - it currently does not work great on complex pages.
  - Store them in a temporal folder at `OUTCOME_DIR/01 - Interviews/.tmp/PERSONA_SLUG` (both placeholders are replaced by the main agent when building the prompt). Create the folder if it does not exist and delete it when the interview is done
  - Only use snapshots when
    - (1) screenshots were not produced in a reasonable time
    - (2) screenshots were not enough to complete your task, or
    - (3) the persona does not see the page (e.g. screen-reader user). 
    - Otherwise use screenshots.
  - When using snapshots, use both `-i` and `-C` flags. (e.g `agent-browser snapshot -i -C`)
  - Screenshots are a very valuable source of information so take as many as you need.
```

### Follow-up Deliverable
When you build any prompt for an interview subagent (follow-up or fallback), replace `{{FOLLOW_UP_DELIVERABLE_SECTION}}` in that prompt with the following block to the prompt:

```md
# Deliverable
Append your response to `OUTCOME_DIR/01 - Interviews/PERSONA_SLUG.md`. Add a new follow-up section ("### Follow-up") with the user's question and your answer, so the transcript stays one continuous story. If appropiate, also add a brief explanation of:
- What you would change (i.e. issues you had)
- What you would keep
- What you would improve
- If you were able to answer the question
```