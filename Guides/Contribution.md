# Monopoly SDK Contribution Guide

> **Version**: 1.0.0\
> **Last updated**: 24 June 2025

Thank you for your interest in contributing to the **Monopoly SDK**! Whether you're fixing bugs, adding new features, improving docs, or enhancing tests—your help is appreciated.

This document outlines how to set up the development environment, standards to follow, and the process for submitting changes.

---

## Table of Contents

- [Monopoly SDK Contribution Guide](#monopoly-sdk-contribution-guide)
  - [Table of Contents](#table-of-contents)
  - [1. Code of Conduct](#1-code-of-conduct)
  - [2. Development Environment Setup](#2-development-environment-setup)
  - [3. Project Structure](#3-project-structure)
  - [4. Running Tests](#4-running-tests)
  - [5. Linting \& Formatting](#5-linting--formatting)
  - [6. Committing Changes](#6-committing-changes)
  - [7. Pull Request Checklist](#7-pull-request-checklist)
  - [8. Working on Features](#8-working-on-features)
  - [9. Branching \& Versioning](#9-branching--versioning)
  - [10. Security Reporting](#10-security-reporting)
    - [Happy hacking! 🎲](#happy-hacking-)

---

## 1. Code of Conduct

This project follows the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).

Please be respectful in all interactions. Abusive or inappropriate behavior will not be tolerated.

---

## 2. Development Environment Setup

1. **Clone the repo**:

```bash
git clone https://github.com/monopoly/monopoly-sdk.git
cd monopoly-sdk
```

2. **Install dependencies**:

```bash
corepack enable # enables Yarn Berry
yarn install
```

3. **Bootstrap the project** (if monorepo):

```bash
yarn workspaces foreach run build
```

4. **Build the SDK**:

```bash
yarn build
```

5. **Start dev watcher**:

```bash
yarn dev
```

Node 18+ is required. Use `nvm` or `asdf` to manage versions if needed.

---

## 3. Project Structure

```
monopoly-sdk/
├── packages/
│   ├── sdk/           # main SDK source code
│   ├── ui/            # optional white-label UI components
│   └── ai/            # experimental AI players
├── examples/          # integration examples
├── docs/              # documentation generator
├── .github/           # issue templates, workflows
├── scripts/           # CLI tools for maintainers
└── jest.config.ts     # test config
```

---

## 4. Running Tests

Unit and integration tests live in the SDK package.

```bash
yarn workspace @monopoly/sdk test
```

Run tests in watch mode:

```bash
yarn test --watch
```

Generate coverage:

```bash
yarn test --coverage
```

---

## 5. Linting & Formatting

This project uses ESLint and Prettier.

```bash
yarn lint
```

Auto-fix issues:

```bash
yarn lint --fix
```

Check formatting:

```bash
yarn prettier --check .
```

Fix formatting:

```bash
yarn prettier --write .
```

---

## 6. Committing Changes

We use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(session): add support for custom dice values
fix(api): handle 401 errors from token endpoint
```

Use the `yarn commit` helper (powered by `commitizen`) to follow the format:

```bash
yarn commit
```

---

## 7. Pull Request Checklist

Before submitting a PR:

- ***

## 8. Working on Features

1. Create a branch:

```bash
git checkout -b feat/some-feature
```

2. Work in the relevant `packages/` subfolder.

3. Write or update tests.

4. Push to your fork and open a PR against `main`.

---

## 9. Branching & Versioning

- The default branch is `main`.
- Releases are managed with [Changesets](https://github.com/changesets/changesets).
- CI will bump versions and publish to npm.

Run this before merging a feature:

```bash
yarn changeset
```

This will prompt you to describe the change and its version impact (patch, minor, major).

---

## 10. Security Reporting

If you find a vulnerability, email us at [security@monopoly.io](mailto:security@monopoly.io). Please do not open GitHub issues for security problems.

---

### Happy hacking! 🎲

Want to add a new board theme, animation, or AI strategy? Go for it! Questions? Open a [discussion](https://github.com/monopoly/monopoly-sdk/discussions) or chat in `#monopoly-dev` on our Discord.
