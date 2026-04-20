# Skill: Kahoot Quiz Generator

## Description
Creates Kahoot-compatible quiz content from transcripts, articles, notes, lesson materials, or teacher-provided key points. The interaction is designed as a **three-response workflow**:
1. **First response**: clarify quiz settings.
2. **Second response**: preview questions and answers, then ask whether to generate the spreadsheet.
3. **Third response**: generate the spreadsheet in Kahoot format. This must be: an actual `.xlsx` file. No other output format is acceptable for response 3 unless the user explicitly asks for a non-xlsx fallback. Anything file which contains "sandbox" in the name or link is considered a failure.

This skill does **not** rely on the user uploading a Kahoot template. It uses the standard Kahoot spreadsheet structure directly. Kahoot's spreadsheet import requires question and answer fields, a supported time limit, and correct-answer numbers in a fixed format.

## When to use
Use this skill when the user asks for a Kahoot quiz

## When to suggest using this skill
Suggest this skill to the user when the user:
- wants quiz questions from a transcript or text,
- wants key points turned into multiple-choice questions,
- wants output in Kahoot spreadsheet/import format,
- is preparing teaching materials, revision tasks, or comprehension checks.

## Three-response workflow

### Response 1: Clarification
The first response should briefly clarify these four settings:
- comprehension difficulty level of the questions,
- number of questions,
- students' English level,
- time limit per question: **5, 10, 15, or 20 seconds**.

#### Clarifying prompt template
Use a short prompt like this:

"Before I generate the Kahoot, please tell me:
- difficulty: easy / medium / hard
- number of questions
- students' English level, e.g. A2, B1, B2
- time limit: 5, 10, 15, or 20 seconds"

If the user already provided some of these, ask only for the missing ones.

If the user wants speed over precision, the AI may assume defaults:
- difficulty: medium
- number of questions: 5
- English level: B1-B2
- time limit: 10 seconds

Any assumptions must be stated briefly.

### Response 2: Preview
The second response should:
1. briefly confirm the chosen settings,
2. show the drafted questions,
3. show the answer options,
4. indicate the correct answer(s),
5. ask the user whether they want the spreadsheet generated.

This response is a **preview only**, not yet the spreadsheet.

#### Preview structure
Recommended structure:
- short line confirming settings,
- numbered list of questions,
- four answer options per question,
- one line showing the correct answer,
- final question such as:  
  **"Would you like me to generate the Kahoot spreadsheet now?"**

### Response 3: Spreadsheet
The third response should generate the spreadsheet output in Kahoot format.

This must be an actual `.xlsx` file if file generation is available. If this is not possible, inform user and output as table. Never return a fake xlsx file such as "sandbox".

The spreadsheet must follow Kahoot's standard import structure with fixed columns and answer-number notation. Kahoot's support guidance states that spreadsheet imports require at least two answers, valid time-limit values, and correct answers indicated by answer number, for example `1` or `2,3`.

## Core workflow
1. Read the source text carefully.
2. Identify the main ideas, examples, claims, and contrasts.
3. Select the most useful key points for the target learners.
4. Generate the requested number of multiple-choice questions.
5. Adapt wording and distractors to the stated comprehension level and English level.
6. In response 2, preview the questions and answers.
7. In response 3, generate the spreadsheet.
8. End the spreadsheet response with a very brief guide for using it in Kahoot.

## Key-point selection rules
Prioritise points that are:
- central to the speaker's argument,
- supported by examples,
- useful for comprehension checking,
- distinct from each other,
- appropriate for the students' level.

Avoid choosing several questions that all test the same idea.

## Difficulty guidance

### Easy
Use when learners need straightforward recall and basic understanding.
- Ask about main ideas, examples, definitions, or clearly stated claims.
- Use simple wording.
- Make distractors clearly wrong but still plausible.

### Medium
Use when learners can handle paraphrase and comparison.
- Ask about cause/effect, contrast, speaker viewpoint, examples, or implications.
- Rephrase parts of the source instead of copying them directly.
- Make distractors plausible enough to require attention.

### Hard
Use when learners can infer, synthesise, and interpret.
- Ask about nuance, analogy, implication, argument structure, or unstated meaning.
- Use closer distractors.
- Require distinction between similar claims.

## English-level adaptation

### Lower levels (A2-B1)
- Use short sentences.
- Prefer frequent vocabulary.
- Avoid idioms unless they are part of the learning goal.
- Keep answer options clearly different.

### Middle levels (B1-B2)
- Use normal classroom English.
- Allow some paraphrase and abstract vocabulary.
- Keep options concise and readable.

### Higher levels (B2-C1+)
- Use more precise wording.
- Include inference, tone, implication, and argument structure.
- Distractors may be more closely related.

## Standard Kahoot spreadsheet format
Always use this exact column order:

| Column | Header |
|---|---|
| A | Question |
| B | Answer 1 |
| C | Answer 2 |
| D | Answer 3 |
| E | Answer 4 |
| F | Time limit sec |
| G | Correct answers |

Kahoot's spreadsheet import documentation and help materials describe this fixed structure, along with answer-number marking and character limits for questions and answers.

### Header rules
- **Question**: maximum 95 characters
- **Answer 1-4**: maximum 60 characters each
- **Time limit sec**: use one of the values requested by the user, limited here to **5, 10, 15, or 20**
- **Correct answers**: answer number(s), e.g. `2` or `1,3`

Kahoot support materials list spreadsheet constraints including 95 characters for questions, 60 for answers, and correct answers entered as answer numbers separated by commas where needed.

## Question-writing rules
- Each question should test one key point only.
- Use exactly 4 answer options unless the user asks otherwise.
- Include at least 1 correct answer.
- Distractors must be plausible but clearly inferior to the correct answer.
- Avoid trick questions.
- Avoid negative wording unless necessary.
- Avoid copying long chunks from the source text.
- Prefer paraphrase over quotation.
- Keep wording concise for fast classroom reading.

## Recommended internal process
1. Extract more candidate points than needed.
2. Choose the strongest set for coverage and variety.
3. Draft questions.
4. Check readability against learner level.
5. Shorten questions and answers to fit Kahoot character limits.
6. Verify correct-answer numbering.
7. Present preview in response 2.
8. Generate spreadsheet in response 3 only after user approval.

## Response-specific behaviour

### Response 1 rules
- Ask for the four settings only.
- Keep it short.
- Do not generate questions yet unless the user explicitly says to assume defaults.

### Response 2 rules
- Present the draft clearly for teacher checking.
- Include correct answers visibly.
- Do not generate the spreadsheet yet.
- End with a direct confirmation question:
  **"Would you like me to generate the spreadsheet now?"**

### Response 3 rules
- Produce only the spreadsheet file plus a very brief Kahoot guide.
- Keep the column order exact.
- Do not re-explain the whole process.
- Produce `.xlsx`.

## Spreadsheet output requirements
When generating the final Kahoot content, structure it as a sheet with these columns only:

`Question | Answer 1 | Answer 2 | Answer 3 | Answer 4 | Time limit sec | Correct answers`

Do not reorder columns.

Do not add extra columns.

Do not place explanatory notes inside the sheet.

When creating an actual spreadsheet file, use a descriptive filename, for example:
- `kahoot_automation_quiz.xlsx`
- `kahoot_climate_change_b1.xlsx`
- `kahoot_video_transcript_medium_10s.xlsx`

## Validation checklist
Before finalising, always check:
- [ ] correct column order,
- [ ] all questions fit within 95 characters,
- [ ] all answers fit within 60 characters,
- [ ] time limit uses the requested value,
- [ ] correct answer numbers match the answer positions,
- [ ] question difficulty matches the requested level,
- [ ] English matches the students' level,
- [ ] question set covers distinct key ideas,
- [ ] response 2 is preview-only,
- [ ] response 3 is the spreadsheet output.

## Very brief Kahoot guide
At the end of the **third response only**, include this guide: "https://create.kahoot.it/creator -> Blank canvas -> Add -> Import -> Import spreadsheet -> delete the first question as it is now blank -> name the Kahoot -> save"

Kahoot's own help pages describe creating a quiz, choosing the import option, and uploading a `.xlsx` spreadsheet for question import.
## Example interaction

### Example response 1
"Before I generate the Kahoot, please tell me:
- difficulty: easy / medium / hard
- number of questions
- students' English level
- time limit: 5, 10, 15, or 20 seconds"

### Example response 2
"I’ll use medium difficulty, 5 questions, B1-B2 English, and 10 seconds.

1. What is the speaker's main argument?
A. ...
B. ...
C. ...
D. ...
Correct answer: C

2. ...

Would you like me to generate the spreadsheet now?"

### Example response 3
Provide the Kahoot sheet as an `.xlsx` file. This must be: an actual `.xlsx` file. No other output format is acceptable for response 3 unless the user explicitly asks for a non-xlsx fallback. Anything file which contains "sandbox" in the name or link is considered a failure. Then add: "https://create.kahoot.it/creator -> Blank canvas -> Add -> Import -> Import spreadsheet -> delete the first question as it is now blank"

## Good defaults
- Difficulty: medium
- Number of questions: 5
- English level: B1-B2
- Time limit: 10 seconds
- Number of answers per question: 4

## Style guidance
- Be direct and teacher-friendly.
- Optimise for practical classroom use.
- Keep formatting clean and reusable.
- Prefer clarity over cleverness.

## Important constraints
- Do not require the user to upload a Kahoot template.
- Do not output a markdown table when the user explicitly asks for a sheet.
- Do not add extra spreadsheet columns.
- Do not exceed Kahoot character limits.
- Do not skip the preview step.
- Do not generate the spreadsheet before the user confirms after the preview.

## Deliverables
Depending on the step in the workflow, produce one of the following:
- response 1: clarification prompt,
- response 2: preview of questions and answers,
- response 3: `.xlsx` file, plus a brief Kahoot guide. This must be: an actual `.xlsx` file. No other output format is acceptable for response 3 unless the user explicitly asks for a non-xlsx fallback. Anything file which contains "sandbox" in the name or link is considered a failure.

---
Created from iterative classroom-use refinement. Designed for a staged teacher workflow: clarify, preview, then export.
