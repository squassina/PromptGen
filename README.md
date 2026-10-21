# ✨ Beginner Prompt Generator

A single-file web tool that transforms simple answers into **well-structured
prompts**, ready to copy and paste into any AI (Claude, ChatGPT, Gemini, etc.).

Built for anyone who **has never studied prompt engineering**: no jargon, helpful
examples in every field, real-time guidance, and one-click copy.

> No installation, no dependencies, no server required. Just open the file in
your browser.

---

## Table of Contents

- [Features](#features)
- [How to Use](#how-to-use)
- [Available Modes](#available-modes)
- [What the Generated Prompt Contains](#what-the-generated-prompt-contains)
- [Running Locally](#running-locally)
- [Customization](#customization)
- [Privacy](#privacy)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [License](#license)

---

## Features

| Feature | What It Does |
| --- | --- |
| **Plain Language Questions** | Replaces technical jargon with direct questions and helpful placeholder examples. |
| **Essential Fields First** | Only essential fields appear initially; optional inputs are kept in a collapsible section. |
| **Quick Choice Chips** | Select tone and response format with a single click. |
| **Fill with Example** | Shows how a completed, high-quality prompt looks in action. |
| **Quality Meter** | Rates prompts as *Basic*, *Good*, or *Excellent* and suggests missing details. |
| **Editable Prompt** | The generated text can be manually edited before copying. |
| **Edit Protection** | If you make manual edits, field changes won't overwrite them unless you click **Update from fields**. |
| **Auto-Save** | Form fields are saved locally in your browser so you can resume anytime. |
| **Light & Dark Theme** | Automatically adapts to your system theme preference. |
| **Responsive & Accessible** | Optimized for desktop and mobile, with visible focus states and screen reader support. |

## How to Use

1. **Select** what you want to achieve (write, research, or code).
2. **Fill in** the fields. Only the first field marked with `*` is required.
3. **Copy** the prompt and paste it into your preferred AI model.

Tip: If the AI responds with follow-up questions, that is by design. The prompt
instructs the model to ask clarifying questions before assuming details when
critical context is missing. Answer them for a higher-quality response.

## Available Modes

### ✍️ Write & Plan
For emails, articles, plans, and creative ideas.
Fields: task, context, target audience, tone, format, and expert role (optional).

### 🔎 Research & Analyze
For summaries, comparative analyses, and reports.
Fields: main question, audience, **information source**, source material to
analyze, timeframe or region, and format.

The selected information source defines the evidence guidelines embedded in the
prompt:

- **AI Knowledge:** The AI flags uncertainties and clearly separates facts from
interpretations.
- **Web Search:** The AI cites sources and verifies key facts. Requires web
access enabled in the target AI model; if unavailable, it will inform you rather
than simulating search.
- **Provided Material Only:** The AI strictly avoids external knowledge and
highlights anything missing from the provided text.

### 💻 Coding
For debugging, writing new features, or explaining code.
Fields: problem description, programming language or tool, code snippet or error
message, expected result, constraints, and response style (e.g., "explain step by
step").

## What the Generated Prompt Contains

Prompts are constructed using proven prompt engineering techniques:

- **Markdown structure** with clear section headings (`# Task`, `## Context`,
`## Response Format`, etc.).
- **XML Delimiters** (`<material>`, `<code>`, `<context>`) to isolate user
inputs from system instructions. Always used for source materials and code; used
for context when text is multiline or detailed.
- **Clarification safeguard:** Instructs the AI to ask up to 3 concise questions
if critical info is missing.
- **Anti-hallucination constraints:** Explicitly forbids making up facts, statistics,
sources, libraries, or test outputs.
- **Prompt injection protection:** In provided material mode, pasted content is
- explicitly treated as data, not executable instructions.
- **Explicit output specifications**, defined by you or defaulted to sensible standards.

<details>
<summary>Example generated prompt ("Write & Plan" mode)</summary>

```markdown
Act as a financial manager specializing in customer relations.

# Task
Write a polite email following up on an overdue invoice

## Context
Customer for 2 years. $1,200 invoice was due on the 10th. Never late before.

## Audience
Small business owner, our client

## Tone
Friendly

## Response Format
Ready-to-send email with a subject line

## Guidelines
- If essential information is missing, ask up to 3 concise questions before responding.
- Do not invent facts, numbers, names, or deadlines; flag anything missing.
- Deliver a ready-to-use result in clear, direct language.
```

</details>

## Running Locally

No build step or external dependencies required.

```bash
git clone https://github.com/squassina/PromptGen.git
cd PromptGen
```

Simply double-click `index.html` to open it in your browser, or start a
lightweight local web server:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000/index.html
```

## Customization

All form structure and UI text are contained within a single JavaScript object
named `M` located inside the `<script>` tag. To edit fields, labels, examples,
or choices, modify this structure:

```js
{
  id: 'tone',                  // field identifier
  l: 'What tone do you prefer?', // displayed label
  h: 'Optional.',              // help text (optional)
  req: 1,                      // required field flag
  area: 1,                     // renders textarea instead of input
  adv: 1,                      // places field in the optional section
  chips: ['Friendly', 'Direct'], // quick selection chips
  ph: 'e.g., Professional...',  // input placeholder
  tip: 'choose a tone'         // recommendation hint for quality meter
}
```

To adjust how final prompt outputs are assembled, edit the `build()` function
and the `SRC` object (search and evidence rules).

To create a brand-new operational mode, add a new entry to `M` (including `n`,
`d`, `fields`, and `ex`) and handle its output logic inside `build()`.

## Privacy

- Execution happens **100% locally inside your browser**. No user data is sent to
external servers.
- Form states are saved exclusively in your browser's `localStorage` (key `gp-v4`).
Use **Clear fields** or purge site storage to remove saved data.
- The app makes zero external network API calls and relies on zero third-party libraries.
- Avoid pasting API keys, passwords, or confidential data into fields, as final
prompt outputs are intended to be sent to external AI providers.

## Project Structure

```text
.
├── index.html   # Complete single-file app (HTML, CSS, JS)
└── LICENSE
└── README.md
└── README.BR.md
```

## Contributing

Contributions, feature requests, and improvements are welcome!

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/my-improvement`.
3. Commit your changes: `git commit -m "Add new feature"`.
4. Push to origin: `git push origin feature/my-improvement`.
5. Open a Pull Request.

Ideas for future enhancements: new modes (marketing, education, customer service),
`.txt` download options, prompt history logging, multi-language switching, and
automated test coverage.

When contributing, please maintain a strong focus on **simplicity for beginners**:
clear language, minimal mandatory inputs, and helpful guidance.

## License

This project runs under [MIT Licence](LICENSE).
