# diego-code-style-skill

Personal coding style skill focused on readability, structure, and maintainable TypeScript/React code.

---

## ✨ Overview

This repository contains a **personal coding style skill** designed to enforce:

- clean and readable code
- consistent file and component structure
- strong TypeScript practices
- scalable React architecture
- maintainable and well-organized codebases

The goal is simple:

> Write code that is easy to read, easy to reason about, and easy to maintain.

---

## 📦 Installation

Clone or download this repository:

```bash
git clone https://github.com/<your-username>/diego-code-style-skill.git
```

Then copy the skill into your global skills directory:

```bash
mkdir -p ~/.agents/skills/diego-code-style
cp SKILL.md ~/.agents/skills/diego-code-style/SKILL.md
```

---

## 🧠 Usage

Once installed, the skill can be used automatically by your AI agent or explicitly referenced in prompts.

Example:

> "Create a React component following my code style"

or

> "Refactor this file using my coding style skill"

---

## 🧩 What this skill enforces

### Code quality
- readability over cleverness
- simple and explicit logic
- clear separation of concerns

### Structure
- consistent file organization
- logical grouping of code sections
- modularization when needed

### TypeScript
- strict typing
- no `any` unless absolutely necessary
- types grouped and imported properly

### React
- `React.FC` components
- arrow functions
- clean render (minimal logic inside JSX)
- proper use of hooks and memoization

### Comments
- meaningful documentation
- multiline comments with consistent format
- explanation of complex logic

### Formatting
- logical spacing between code blocks
- paragraph-style separation for readability

---

## 📁 Example Structure

```
component/
├── main-component.tsx
├── main-component.types.ts
├── main-component.constants.ts
├── main-component.utils.ts
├── main-component.styles.ts
└── parts/
    ├── sub-component-a.tsx
    └── sub-component-b.tsx
```

---

## ⚙️ Philosophy

This style is based on a few core ideas:

- Code should read like a book
- Structure should be predictable
- Logic should be easy to follow
- Complexity should be isolated
- Maintenance should be effortless

---

## 🚀 When to use

Use this skill when:

- creating new components
- refactoring code
- reviewing or improving structure
- enforcing consistency across a codebase

---

## ⚠️ Important Note

When modifying existing files:

- preserve the current structure
- avoid unnecessary refactors
- only restructure when explicitly required

---

## 📄 License

MIT (or your preferred license)

---

## 👨‍💻 Author

Diego
