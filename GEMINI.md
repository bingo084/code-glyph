# `CodeGlyph` Project Context

## Project Overview

`CodeGlyph` is a single-page web application for practicing character-based typing, specifically designed for input methods that use letter codes (e.g., Rime-based methods like Wubi or custom phonetic schemes). It helps users memorize character encodings by leveraging a Spaced Repetition System (SRS).

The entire application is self-contained within a single `.html` file, using vanilla HTML, CSS, and JavaScript. It has no external dependencies and requires no build process.

### Core Features

*   **Practice Modes**: Users can select from pre-defined practice texts (Top 500/1000/1500 most common Chinese characters) or paste their own custom text.
*   **Dictionary System**: Supports a pre-defined online dictionary ("飞单") fetched from a URL, or custom dictionaries uploaded by the user in the Rime `.dict.yaml` format.
*   **Spaced Repetition System (SRS)**: The application tracks user performance for each character. Correct answers increase a character's mastery level and schedule its next review further in the future. Incorrect answers decrease the level and schedule an imminent review.
*   **Per-Profile Progress**: Learning progress is stored independently for each dictionary. This means a user's stats for the "飞单" dictionary are kept separate from their stats for a "custom" uploaded dictionary.
*   **State Persistence**: The application uses the browser's `localStorage` to remember:
    *   The last selected dictionary and practice text.
    *   All learning progress, stored in separate profiles.
*   **Advanced Input Validation**:
    *   **Strict Mode**: Input is validated on every keystroke. If the typed sequence is not a valid prefix of any correct code for the current character, it is immediately marked as incorrect.
    *   **Shortest Code Hint**: If a character has multiple correct codes, and the user enters a valid but non-optimal (i.e., not the shortest) one, a hint displaying the shortest code is shown before proceeding.
    *   **On-Demand Hints**: Users can press `Space` (if the input field is empty) or `ArrowDown` at any time to get a hint.
*   **Polished UX**: Includes a modern UI, non-blocking status notifications, a "Return to Main Menu" button during practice, and a "Clear Progress" function with a confirmation dialog.

## Building and Running

*   **Build**: No build step is required.
*   **Run**: Open the `index.html` file (or `CodeGlyph-v2.html`) directly in any modern web browser.
*   **Test**: There are no automated tests. Functionality is verified by manually using the application in the browser.

## Development Conventions

*   **File Structure**: The entire application is encapsulated in a single `.html` file.
*   **Styling**: CSS is located in a `<style>` block in the `<head>`. It uses CSS variables (e.g., `--primary-color`) for theming.
*   **Scripting**: All JavaScript code resides in a `<script>` block at the end of the `<body>`.
    *   A global `DOM` object is used to cache references to frequently accessed DOM elements.
    *   Global-like variables hold application state (`dictionary`, `practiceSet`, `glyphStats`, `currentProfileId`).
    *   Logic is organized into functions based on features (e.g., `handleDictSelection`, `startPracticeSession`, `handleCorrectAnswer`).
*   **Data Persistence**:
    *   The primary storage key is `codeGlyphProfiles` in `localStorage`. This key holds a JSON string representing an object where each key is a profile ID (e.g., "custom", "feidan") and each value is the corresponding `glyphStats` object for that profile's progress.
    *   `lastDictSelection` and `lastTextSelection` keys store the user's last chosen dropdown options.
