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
- Always separate language structures such as `if`, `else`, `switch`, `for`, `for...of`, `forEach`, `while`, and similar constructs from the statements before them with a blank line.
- Also separate consecutive control-flow structures from one another with blank lines when they represent distinct logical steps.

Preferred style:

```ts
const separatorIndex = segment.indexOf("=");

if (separatorIndex <= 0) {
  return;
}
```

### Exception for very small functions and methods

- If the full body of a function-like block is very short, do not force paragraph-style spacing.
- This exception applies when the total content inside the function, method, handler, memo callback, callback, effect callback, or similar function-like entity is **3 lines or fewer**.
- In those cases, keep the logic together without blank lines, even if it could be interpreted as separate logical groups.
- Apply this exception to:
  - regular functions
  - arrow functions
  - class methods
  - handlers
  - `useMemo`
  - `useCallback`
  - effect callbacks
  - similar callback bodies

Preferred style for short bodies:

```ts
const generatedJson = useMemo(() => {
  const authJson = buildAuthJson(rawInput);
  return stringifyAuthJson(authJson);
}, [rawInput]);
```

- Once the function-like body becomes longer than 3 lines, resume using paragraph-style spacing between distinct logical groups.

## Comments for Complex Logic

- Whenever code includes tricky logic, a hack, a workaround, a fix, or anything not immediately obvious, add a short explanatory comment.
- Prefer a single-line comment when possible.
- Use multiline comments only when necessary.
- The purpose of the comment is to explain **why** the code exists, not just what it does.

## Preserve Existing Structure Unless Asked

- When modifying an existing file, preserve its current overall structure unless the prompt explicitly asks for a structural refactor or the change truly requires it.
- Heavy structural changes (custom hooks, splitting files) apply mainly to **new files created by the AI**.
- For existing files, prefer minimal structural disruption.

# File Structure and Organization

## Section Ordering

1. Imports
2. Interfaces
3. Types
4. Constants
5. Helpers
6. Main component
7. Secondary components
8. Exports
9. Styles

## Section Labels

- Use section comments only when grouping multiple elements.
- Avoid redundancy with multiline comments.

## Import Ordering

1. Core/global dependencies
2. Main libraries
3. Complementary third-party modules
4. Utilities/helpers
5. Enums
6. Types
7. Side-effect-only imports

Important:

- **All type imports must be grouped at the very end of the regular import block**, regardless of source.
- This includes types from main libraries such as `react` or `react-native`.
- Always use `import type`.
- There is one exception after type imports: **side-effect-only imports** that are not assigned to a variable, such as CSS imports.
- These side-effect-only imports must go after all type imports.
- Add a blank line before the side-effect-only import group.

Preferred style:

```ts
import React from "react";
import { View } from "react-native";
import clsx from "clsx";

import { someHelper } from "@/utils/some-helper";

import { Status } from "./component.enums";

import type { FC } from "react";
import type { ViewStyle } from "react-native";
import type { ComponentProps, AnotherType } from "./component.types";

import "./globals.css";
```

## Constants Outside Components

- Use uppercase with underscores.

## File Size

- Prefer modularization for large files (>300 lines), mainly for new files.

## Splitting Rules

- >3 helpers → utils file
- >5 types → types file
- >5 constants → constants file
- Only enforce aggressively for new files.

## Component File vs Folder

- Self-contained → single file
- With dependencies → folder

## Parts

- Use `parts/` for internal subcomponents.

# TypeScript and JavaScript

## Functions

- Prefer arrow functions.

## Comments

### TypeScript

- Multiline comments only (no JSDoc)
- Components/classes/hooks:
  - title
  - description
- Helpers:
  - description only

Format:

```ts
/*
 * Utility function: Parses a cookie header into a key/value map.
 */
```

### JavaScript

- Use JSDoc

# React Rules

## Components

- Arrow function + React.FC
- Prefer React.FC<Props>
- Export separately

## Classnames / cn usage

- Always use `clsx`, `classnames`, or project utility (e.g. `cn`).
- Prefer passing class strings directly into `cn`.

Avoid:

```tsx
<div className={cn(PAGE_CONTENT_CLASS_NAME)}>
```

Preferred:

```tsx
<div className={cn("page-content")}>
```

- Avoid unnecessary indirection through constants when the class string is simple and static.
- Use variables only when they add real value (reuse, complexity, or dynamic composition).

## JSX Element Spacing

- Add blank lines between sibling JSX elements when at least one of them is multiline.
- If two adjacent JSX elements are both single-line, they may remain together without a blank line.
- If either element spans multiple lines, add a blank line between them to improve visual separation.
- Apply this rule broadly to JSX/TSX markup so the structure is easier to scan and not visually crowded.

Avoid:

```tsx
<header className="space-y-2">
  <p className="text-xs font-semibold tracking-[0.16em] text-slate-600 uppercase">
    Utility App
  </p>
  <h1 className="text-3xl font-semibold tracking-tight text-slate-900 sm:text-4xl">
    Convert Browser Tokens to JSON
  </h1>
  <p className="max-w-3xl text-sm leading-relaxed text-slate-600 sm:text-base">
    Copy the value of the <span className="font-mono">Cookie</span> request header from
    Chrome DevTools Network and transform it into auth JSON in one click.
  </p>
</header>
```

Preferred:

```tsx
<header className="space-y-2">
  <p className="text-xs font-semibold tracking-[0.16em] text-slate-600 uppercase">
    Utility App
  </p>

  <h1 className="text-3xl font-semibold tracking-tight text-slate-900 sm:text-4xl">
    Convert Browser Tokens to JSON
  </h1>

  <p className="max-w-3xl text-sm leading-relaxed text-slate-600 sm:text-base">
    Copy the value of the <span className="font-mono">Cookie</span> request header from
    Chrome DevTools Network and transform it into auth JSON in one click.
  </p>
</header>
```

## Render

- Keep render simple
- Move logic out of JSX

## Render Comments

- Only when meaningful, not obvious.

# Internal Component Structure

1. States
2. Memoized values
3. Constants
4. Handlers
5. Helpers
6. Effects
7. Layout effects

- Use section comments only when grouping multiple items.

## Memoization

- Use when beneficial, not blindly.

# Logic Extraction

## Helpers

- Extract heavy logic, mainly in new files.

## Custom Hooks

- Use for large, tightly coupled logic.
- Prefer for new files, not forced in existing ones.

# React Native

- Styles at bottom
- Add section comment only if useful

# Naming

- kebab-case files
- component.utils.ts
- component.types.ts
- component.constants.ts
- component.styles.ts



## Export Spacing

- Never place export statements immediately attached to other structures such as components, functions, or classes.
- Always add a blank line before any export statement unless it is directly grouped with another export.
- Export blocks should be visually separated from implementation code.

Avoid:

```ts
const Component = () => {
  ...
};
export { Component };
```

Preferred:

```ts
const Component = () => {
  ...
};

export { Component };
```

- This applies to:
  - named exports
  - default exports
  - grouped exports

# Decision Rules

1. Readability first
2. Clean structure
3. Minimal render logic
4. Modularize when needed
5. Use hooks for complex logic
6. Stay consistent
7. Break rules only with strong reason
8. Preserve structure when editing existing files
9. Use spacing to separate logic groups
10. Avoid redundant comments
11. Avoid unnecessary className indirection when using `cn`
12. Put side-effect-only imports after type imports, with a blank line before them
13. Add blank lines between sibling JSX elements whenever one of them is multiline
14. Skip paragraph-style spacing inside very short function-like bodies with 3 lines or fewer

# Final Guidance

- Follow intent, not just rules
- Optimize for maintainability
