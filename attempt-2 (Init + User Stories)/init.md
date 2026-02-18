You will be in charge of reproducing an accessibility test in [this site](scope.md#website). The idea is to get a list of user stories that will need to be done to improve that site in terms of accessibilty for a range of different types of users.

For that, certain steps need to be followed. Those are listed below.

# 00 - Personas
- Create or use a folder named `00 - Personas`
- For each of the scenarios, create a Markdown file that will describe how the persona behaves interacting with the website.
- Feel free to spin up a Subagent to do write up each of these personas
- Each persona must have:
  - Instructions for a subagent to explicitly become that persona
  - A profile
  - Behavior Rules
  - What it must do and it must not do
  - How to interact with the website
- All these are needed as each persona will interact differently with the website.
- After the persona description, add steps on what should be changed to improve the persona's experience in the website

The scenarios are:
- ADHD
- Blue-yellow color blind
- Cognitive Disability
- Dyslexic
- Low Contrast Sensibility
- Low vision screen magnifier
- Low vision
- Motion Sensitiviy
- Motor impariment
- Non-native
- Red-green color blind
- Screen-reader user
- Senior person
- Situational Contrast
- Skeptical user
- Voice-control user

# 01 - Interviews & Reports
- Create or use a folder named `01 - Interviews`
- For each of the personas listed in `00 - Personas`, spin up a subagent that will impersonate each persona and request them to do the listed steps in [here](scope.md#goals) 
- The interviews must be created as a Markdown file in `01 - Interviews` and the technical details about what to improve should be put as a Markdown file in `02 - Reports`

# 02 - Actionable Items
Once all the reports are done, based on all of them, create a Main Report (named `_main-report.md`) in the same folder which will include a summary of all the items and give them a priority and a possible estimate based on the work.

# 03 - User stories
Once the main report is done, please create a user story for each of the actionable items listed on the main report. These user stories should include a way to test the change and developer notes on how it can be achieved.