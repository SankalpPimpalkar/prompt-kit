# Prompt Kit

Prompt Kit is a curated collection of reusable AI prompts designed for software developers to generate technical documentation, code reviews, and project workflows across AI-assisted development environments. The repository provides structured instruction templates that eliminate ambiguity and non-deterministic behavior in AI coding assistants such as Cursor, GitHub Copilot, Antigravity, and Claude Code. Its primary design concept is constraint-driven prompting: developers copy and paste prompt files directly into any LLM environment to achieve consistent, verified technical outputs without manual prompt configuration.

## Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Core Components](#core-components)
  - [1. README Generator (`readme-generator.md`)](#1-readme-generator-readme-generatormd)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Usage Examples](#usage-examples)
  - [Generating a Repository README](#generating-a-repository-readme)
- [How It Works](#how-it-works)
- [Project Roadmap & Commit History](#project-roadmap--commit-history)

## Project Overview

AI coding assistants frequently produce inconsistent, unverified, or hallucinated outputs when given unstructured prompts. Prompt Kit solves this by establishing standardized, constraint-based prompt templates that require AI tools to base their analysis strictly on verified repository contents, code files, and git history.

1. **Factual Grounding**: Directives prohibit hallucinated features, unverified commands, and nonexistent files.
2. **Deterministic Formatting**: Strict structural rules enforce uniform heading hierarchies, syntax tags, and concise technical tone.
3. **IDE Agnostic**: Standard Markdown format ensures native compatibility across modern AI IDEs and command-line LLM agents.
4. **Zero Overhead**: Prompts function out of the box with no runtime dependencies or build steps.

## Key Features

- **Standardized Prompt Specifications**: Reusable templates for common development tasks.
  - **README Generation**: Enforces an 11-stage project documentation schema with verified code excerpts and installation steps.
  - **Negative Constraints**: Disallows marketing language, unverified claims, and em dashes.
- **Cross-Platform Portability**: Compatible with Cursor, Windsurf, Antigravity, GitHub Copilot, and LLM chat interfaces.
- **Extensible Architecture**: Clean folder layout structured to support upcoming prompt modules for docs, reviews, and workflows.

## Core Components

### 1. README Generator (`readme-generator.md`)

`readme-generator.md` instructs an AI assistant to analyze project source code, file trees, dependencies, and git history to generate an accurate, production-grade `README.md` file. It enforces strict verification checks before output generation.

| Name | Implementation | Behavior |
| :--- | :--- | :--- |
| `FORMAT RULES` | Markdown and style constraints | Mandates clean tables, fenced code blocks, technical conciseness, and no em dashes. |
| `STRUCTURE` | 11-step ordered layout | Enforces Title, Intro, Table of Contents, Overview, Features, Components, Structure, Setup, Examples, How It Works, and Roadmap. |
| `CHECKS BEFORE FINISHING` | Post-generation verification | Validates that every referenced file, command, code snippet, and anchor link exists. |

```markdown
Analyze this entire project (source files, folder structure, dependencies, scripts, git history if available) and write a README.md in the exact format below. Base everything on the actual code. Do not invent features, files, results, or commands. If something cannot be verified from the repo, leave it out.

FORMAT RULES
- Markdown with clean headings, tables, and fenced code blocks (with language tags).
- Use LaTeX ($...$) only if the project involves math.
- Keep descriptions concise and technical. No filler, no marketing language.
- Do not use em dashes.
```

## Project Structure

```text
prompt-kit/
|-- readme-generator.md  # Template prompt for generating repository README files
`-- README.md            # Project documentation generated from readme-generator.md
```

## Installation & Setup

### Prerequisites

- Git
  - macOS: `brew install git`
  - Ubuntu/Debian: `sudo apt-get install git`
  - Windows: `winget install --id Git.Git -e --source winget`

### Clone Repository

```bash
git clone https://github.com/SankalpPimpalkar/prompt-kit.git
cd prompt-kit
```

No additional dependencies, package managers, or build steps are required.

## Usage Examples

### Generating a Repository README

1. Open your target repository in an AI-assisted IDE (such as Cursor, Windsurf, or Antigravity).
2. Load the contents of `readme-generator.md` into the AI context window, or attach the file directly.
3. Submit the prompt directive:

```text
@readme-generator.md Analyze this repository and generate a README.md following the specification.
```

4. Verify the generated output against the built-in completion checklist.

## How It Works

1. **Context Ingestion**: The AI agent reads the target project directory, configuration files, source code, and git log alongside `readme-generator.md`.
2. **Constraint Application**: The model applies formatting and style rules, rejecting ungrounded assumptions and informal prose:
   ```markdown
   - Keep descriptions concise and technical. No filler, no marketing language.
   - Do not use em dashes.
   ```
3. **Sequential Section Generation**: The agent generates sections 1 through 11 in order, embedding real code snippets and accurate directory trees.
4. **Validation Pass**: The assistant checks the final output against repository reality before writing the file:
   ```markdown
   CHECKS BEFORE FINISHING
   - Every file mentioned in the README exists.
   - Every command and code snippet matches the actual code.
   - The table of contents links match the headings.
   - Remove any section that does not apply to this project instead of leaving it empty.
   ```

## Project Roadmap & Commit History

### Commit History

1. **Milestone 1: Repository Foundation and README Generator Prompt** (`cc81ded`)
   - Added `readme-generator.md` defining the 11-step README structure, formatting rules, and verification checklist.

### Planned Roadmap

- **Milestone 2: Documentation Generator (`docs-generator.md`)**
  - Standardized prompts for API reference docs, architecture decision records, and contribution guides.
- **Milestone 3: Code Review Assistant (`code-review.md`)**
  - Prompts for automated pull request reviews, security vulnerability scanning, and code quality analysis.
- **Milestone 4: Workflow Automation Prompts (`workflow-generator.md`)**
  - Prompts for generating CI/CD pipelines, pre-commit configurations, and automated release scripts.
