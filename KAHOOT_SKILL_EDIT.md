# Skill: Kahoot Skill Editor

## Description
Edits and re-customises `KAHOOT_SKILL.md` or a subsequent customised version of that skill for a teacher's own subject area, level range, and preferred defaults. This is a **four-response workflow**:
1. check that a base Kahoot skill file is available and warn clearly if it is not,
2. ask what subject or subjects the teacher teaches,
3. ask what level or levels they teach,
4. ask for preferred defaults for number of questions and time per question,
5. output a revised markdown skill file based on the visible Kahoot skill file, plus a brief note on how to save and use it.

This skill is for adapting the original Kahoot skill, not for generating quiz questions directly.

## When to use
Use this skill when the user wants to adapt `KAHOOT_SKILL.md` or a later customised version of it for a different teaching context, subject area, learner profile, or classroom default.

## Core requirement
The AI must first make sure it can see a Kahoot skill source file in the current chat.

Accepted source files include:
- `KAHOOT_SKILL.md`
- `KAHOOT_SKILL_CUSTOM.md`
- another clearly named later version of the Kahoot skill, such as a subject-specific or revised variant

If no suitable Kahoot skill file is visible, the AI must stop and say clearly:

"I can't see a Kahoot skill markdown file in this chat yet. Please upload `KAHOOT_SKILL.md` or a later customised version, then I can adapt it for you."

Do not guess the contents of the source file if it is missing.

## Workflow

### Response 1: File check + subjects
The first response must:
- check whether a suitable Kahoot skill markdown file is available in the current chat,
- use the most appropriate visible version as the source file, normally the latest or most clearly relevant one,
- warn the user if no suitable source file is visible,
- if it is available, ask only this question:

"What subject or subjects do you teach that you want this adapted for?"

Examples the AI may accept:
- EFL
- history
- biology
- translation studies
- software development
- EAP and intercultural communication

Do not ask about levels or defaults yet.

### Response 2: Levels
The second response must ask only this:

"What level or levels do you teach?"

Examples the AI may accept:
- A2-B1
- B2-C1
- secondary school
- first-year undergraduates
- MA students
- mixed ability adult learners

Do not ask about defaults yet.

### Response 3: Defaults
The third response must ask only this:

"What would you like as your defaults for:
- number of questions
- time per question

Please use a Kahoot-supported time limit: 5, 10, 15, or 20 seconds."

If the user gives an unsupported time value, the AI should ask them to choose one of: 5, 10, 15, or 20.

### Response 4: New markdown file
The fourth response must:
- read the visible Kahoot skill source file,
- preserve its useful structure where possible,
- adapt the wording so it matches the user's stated subject(s), level(s), and preferred defaults,
- treat the visible source file as the current base version, even if it is already a customised or revised version,
- output a new markdown file,
- give the file a clear name such as `KAHOOT_SKILL_CUSTOM.md` or another sensible next-version name,
- include a very brief note telling the user to save the markdown as a new `.md` file and upload or drag it into the AI when they want to use that customised version.

If file creation is available, create the adapted markdown as an actual `.md` file.
If file creation is not available, output the full markdown in a fenced code block.

## Editing principles
When adapting the source skill:
- keep the overall classroom workflow unless the user asked for a deeper redesign,
- change references to EFL or English level where needed,
- if English-level wording is no longer suitable, replace it with subject-appropriate level wording,
- update the examples so they match the user's subjects,
- update the defaults section so it reflects the user's chosen number of questions and time limit,
- keep Kahoot spreadsheet constraints intact,
- keep the distinction between preview step and spreadsheet-generation step intact.

## Subject adaptation guidance

### If the subject is still language-related
The AI may keep language-level wording, CEFR examples, and comprehension framing where appropriate.

### If the subject is not language-related
The AI should replace language-specific wording with subject-appropriate wording such as:
- learner level,
- year group,
- course stage,
- degree level,
- prior knowledge,
- conceptual difficulty.

Examples:
- history -> focus on facts, chronology, causes, consequences, interpretation,
- biology -> focus on processes, terminology, systems, functions, comparisons,
- software development -> focus on concepts, syntax, logic, debugging, best practice,
- translation studies -> focus on concepts, methods, terminology, examples, decision-making.

## Output note for response 4
After the new markdown file, add a short note like this:

"Save this as `KAHOOT_SKILL_CUSTOM.md`. Then drag or upload it into the AI together with your source material when you want to use the customised version."

## Style guidance
- Be direct.
- Ask one stage at a time.
- Do not rush ahead to later questions.
- Keep prompts short and teacher-friendly.
- Preserve the practical tone of the original skill.

## Important constraints
- Do not adapt the skill unless a suitable Kahoot skill markdown file is visible.
- Do not ask all setup questions at once.
- Do not ask about levels before subjects.
- Do not ask about defaults before levels.
- Do not output the revised markdown before the user has answered the earlier stages.
- Do not remove Kahoot format constraints from the original skill.

## Example interaction

### Example response 1
"What subject or subjects do you teach that you want this adapted for?"

### Example response 2
"What level or levels do you teach?"

### Example response 3
"What would you like as your defaults for:
- number of questions
- time per question

Please use a Kahoot-supported time limit: 5, 10, 15, or 20 seconds."

### Example response 4
Create `KAHOOT_SKILL_CUSTOM.md` or another sensible next-version file and add:
"Save this as a new `.md` file. Then drag or upload it into the AI together with your source material when you want to use the customised version."

## Deliverables
Depending on the stage, produce one of the following:
- response 1: file check + subject question,
- response 2: levels question,
- response 3: defaults question,
- response 4: adapted `.md` file plus brief save/use note.

---
Created to adapt the Kahoot quiz skill, including later customised versions, across subjects and learner groups.
