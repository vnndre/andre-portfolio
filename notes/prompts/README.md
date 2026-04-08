# Prompts

The actual AI prompts behind the tools in my portfolio. Most of my projects are "vibecoded" — built collaboratively with Claude and ChatGPT — and the prompt is as much a design artifact as the code. These documents capture the prompts in their production form, with notes on why each instruction is there.

## Why document prompts

Prompts rot fast. A well-tuned system prompt represents hours of back-and-forth with a model, and most of that tuning is invisible once the prompt is "done". Writing them down — with the reasoning — is the difference between a tool you can maintain and a tool you have to rebuild from memory when the model changes.

It's also honest work. Anyone claiming to build AI products without showing their prompts is hiding the interesting part.

## Contents

- **[holey-moley-report-prompt.md](./holey-moley-report-prompt.md)** — the Claude prompt that turns a week of review data into a structured Markdown report. Used inside the [weekly-review-bot](https://github.com/vnndre/weekly-review-bot) n8n workflow.
- **[topper-advising-system-prompt.md](./topper-advising-system-prompt.md)** — the system prompt for the Topper GPT-integrated advising chatbot built for St. Edward's students.

*(More coming as I port the v1 custom GPT prompts into this format.)*
