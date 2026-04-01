---
name: diego-code-style
description: Universal coding preferences focused on clarity, structure, consistency, and maintainability across languages, with special emphasis on TypeScript/JavaScript and React-based ecosystems.
---

# Purpose

Use this skill whenever creating, refactoring, or editing code. These are the user's personal coding preferences and should be treated as default implementation standards unless the repository or task explicitly requires a different convention.

Prioritize readability, simplicity, clear structure, and maintainable organization over cleverness or compact code.

# Core Principles

- Always prefer code that is easy to read and understand.
- Favor simplicity and elegance over complexity.
- Use clear intermediate variables instead of deeply nested one-liners.
- Keep logic organized, grouped, and visually easy to scan.
- Use best practices appropriate to the language and framework.
- When a rule cannot be followed exactly due to technical constraints, follow its intent as closely as possible.

# Universal Rules

## Readability First

- Avoid dense expressions when the same logic can be expressed through multiple simple steps.
- Prefer deriving values in clearly named constants instead of chaining multiple calls in a single statement.
- Make the code extremely easy for another developer to read and understand quickly.

## Visual Separation and Paragraph-Style Spacing

- Use blank lines to separate instructions that belong to different logical groups.
- Treat code like written prose with clear paragraph separation.
- Keep together only statements that belong to the same immediate logical group.
- Whenever a new piece of logic starts, add a blank line before it.
- Always separate language structures such as `if`, `else`, `switch`, `for`, `for...of`, `forEach`, `while`, and similar constructs from the statements before them with a blank line, unless they are part of the exact same tightly coupled logical group.
- Also separate consecutive control-flow structures from one another with blank lines when they represent distinct logical steps.

Preferred style:

```ts
const separatorIndex = segment.indexOf("=");

if (separatorIndex <= 0) {
  return;
}
```

## Comments for Complex Logic

- Whenever code includes tricky logic, a hack, a workaround, a fix, or anything not immediately obvious, add a short explanatory comment.
- Prefer a single-line comment when possible.
- Use multiline comments only when necessary.
- The purpose of the comment is to explain **why** the code exists, not just what it does.

## Preserve Existing Structure Unless Asked

- When modifying an existing file, preserve its current overall structure unless the prompt explicitly asks for a structural refactor or the change truly requires it.
- Rules that involve heavier structural changes, such as extracting logic into custom hooks or splitting helpers, constants, types, or styles into separate files, should be treated as defaults for **new files created by the AI**.
- For existing files that are only being edited, prefer minimal structural disruption and keep the file's established organization unless a meaningful refactor is clearly required by the task.

# File Structure and Organization

## Section Ordering

Organize files in this order whenever applicable:

1. Imports
2. Interfaces
3. Types
4. Constants
5. Helpers
6. Main component or main implementation
7. Secondary components or complementary members
8. Exports
9. Styles (when applicable, such as React Native)

## Section Labels

- Before each major group, add a single-line section comment **only when it meaningfully groups multiple related elements**.
- Avoid adding group comments when:
  - There is only a single element in that section.
  - The structure is already obvious.
  - The element already has a descriptive multiline comment.
- Do not combine redundant group comments with multiline documentation blocks.

Example to avoid:

```ts
// Main component

/*
 * Component: Renders a styled button
 */
```

Preferred:

```ts
/*
 * Component: Renders a styled button
 */
```

## Import Ordering

Sort imports by priority from most important to least important using this order:

1. Core/global dependencies
2. Main libraries
3. Complementary third-party modules
4. Utilities and helpers
5. Enums
6. Types

Important rule:

- **All type imports must always be grouped at the very end of the import block**, regardless of which library or module they come from.
- This includes types coming from primary dependencies such as `react`, `react-native`, or any other main library.
- Never place type imports before regular imports, even if the source module is a core dependency.
- Type imports must be grouped together and imported with the `type` keyword when supported.

## Constants Outside Components

- Constants declared outside a component should use uppercase with underscores.

## File Size and Modularization

- If a file becomes too large, especially above 300 lines, strongly consider modularizing it.
- This rule applies most strongly to **new files created by the AI**.
- For existing files, avoid restructuring solely for style consistency unless the prompt asks for it or the change truly requires it.

## Splitting Helpers, Types, and Constants

- >3 helpers → move to utils file
- >5 types → move to types file
- >5 constants → move to constants file
- These split rules apply by default to **new files created by the AI**.
- For existing files being modified, do not introduce this split unless the prompt requests it or the current task clearly benefits from it.

## Component File vs Folder

- Self-contained → single kebab-case file
- With dependencies → folder with associated files

## Parts Directory

- Use `parts/` for internal subcomponents if needed

# TypeScript and JavaScript Preferences

## Functions

- Use arrow functions whenever possible.

## Documentation Comments

### TypeScript
- Use multiline comments (not JSDoc)
- Components/classes/hooks:
  - title (natural language)
  - short description
- Helpers:
  - description only
- Multiline comments must use the starred block format, even if the content is only one line.

Preferred format:

```ts
/*
 * Utility function: Parses a cookie header into a key/value map.
 */
```

Do not use this format:

```ts
/* Utility function: Parses a cookie header into a key/value map. */
```

### JavaScript
- Use JSDoc

# React Rules

## Components

- Arrow function + React.FC
- Prefer React.FC<Props> typing
- Export separately (not inline)

## Multiple Components

- Main first
- Secondary after
- Exports grouped
- Styles after exports if needed

## Classnames

- Use clsx/classnames or project utility (e.g., cn)

## Render

- Keep render simple
- Move logic out of JSX

## Render Comments

- Add comments for UI sections only when they meaningfully describe distinct UI regions.
- Avoid redundant or obvious comments.

# Internal Component Structure

Order:

1. States
2. Memoized values
3. Constants
4. Handlers
5. Helpers
6. Effects
7. Layout effects

- Add section comments only when grouping multiple elements.
- Avoid section comments when there is only one element or when the grouping is obvious.

## Memoization

- Use useMemo/useCallback when useful

# Logic Extraction

## Helpers

- Move heavy logic out of render
- Prefer this by default in **new files created by the AI**
- For existing files, preserve the current structure unless the task explicitly calls for extraction or the change genuinely requires it

## Custom Hooks

- Use when logic is large and tightly coupled
- Prefer this by default in **new files created by the AI**
- For existing files, do not move large portions of logic into a custom hook solely for style consistency unless the prompt requests it or the task requires that refactor

# React Native

- Styles at bottom after exports
- Add // Styles only if it groups multiple style rules meaningfully

# Naming

- Files: kebab-case
- Associated files:
  - component.utils.ts
  - component.types.ts
  - component.constants.ts
  - component.styles.ts

# Decision Rules

1. Prioritize readability
2. Keep structure clean
3. Reduce render complexity
4. Modularize large files
5. Use hooks for complex logic
6. Stay consistent
7. Break rules only with strong reason
8. Preserve existing file structure when editing unless the prompt or task clearly requires structural change
9. Use blank lines to separate distinct logic groups and language structures for better readability
10. Avoid redundant comments when structure or documentation is already clear

# Final Guidance

- Follow these preferences by default
- Respect repo-specific conventions if needed
- Apply intent, not just literal rules
- Optimize for maintainability and clarity
- When editing existing files, prefer minimal and targeted changes over broad structural rewrites unless explicitly requested
