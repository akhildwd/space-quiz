# Copilot instructions for space-quiz

## Project overview
This repository is a small, self-contained web app for a space-themed quiz. The app currently lives in a single file: `index.html`. All markup, styling, and quiz logic are embedded there; there is no framework, package manager, transpile step, or backend.

## Build, test, and lint commands
There are no automated build, test, or lint scripts configured for this repository.

- Manual browser validation: open `index.html` directly in a browser.
- Local static server (recommended for reliable behavior):
  ```bash
  python3 -m http.server 8000
  ```
  Then open `http://localhost:8000`.

For this static app, the practical validation flow is:
1. Load the page and confirm the quiz renders.
2. Answer a few questions and verify the score, progress bar, and feedback text update correctly.
3. Finish the quiz and confirm the result screen and replay flow work as expected.

## High-level architecture
- The app is a DOM-first, single-page experience.
- `index.html` contains three main parts:
  - the HTML structure for the quiz and result screen,
  - an inline `<style>` block for the full visual design and responsive layout,
  - a `<script>` block that defines the quiz content and application behavior.
- The quiz data is stored in a single `questions` array in the JavaScript. Each object follows the same schema:
  - `category`
  - `question`
  - `options`
  - `answer`
  - `fact`
- State is maintained with a few top-level variables: `current`, `score`, and `answered`.
- The main flow is:
  - `renderQuestion()` fills the screen with the current question and option buttons.
  - `chooseAnswer()` handles correct/incorrect responses, updates the score, and shows feedback.
  - `showResults()` swaps the quiz UI for a summary/result state.
  - The replay button resets the session and starts again from the first question.

## Conventions specific to this repo
- Keep the app self-contained in `index.html` unless the project intentionally grows beyond this minimal static structure.
- Preserve the existing question object schema when adding or editing quiz items; do not introduce a different data shape without updating the render logic.
- Prefer the existing design tokens (`--page`, `--card`, `--accent`, etc.) for colors and spacing instead of inventing new hardcoded values.
- Maintain the current accessibility pattern: actual `<button>` elements for choices, clear focus states, and `aria-live` feedback text.
- When changing quiz behavior, keep the existing event-driven flow (`renderQuestion` -> `chooseAnswer` -> `showResults`) and avoid introducing separate component state management.
- This project is intentionally lightweight and static; avoid adding framework, build-system, or dependency complexity unless there is an explicit repo-wide need.

## Files and repo shape
- `index.html`: the entire app.
- No additional source directories, tests, or package manifests are present at the moment.
