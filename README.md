# antigravity-doc-template

English | [繁體中文](README.zh-TW.md)

A standardized documentation template and automated bilingual documentation generator designed for Google Antigravity (AGY) plugins.

Provides comprehensive support across the three core platforms of Google Antigravity (AGY): Antigravity Command-Line Interface (CLI) (`agy`), Antigravity Integrated Development Environment (IDE), and Antigravity 2.0 Desktop Application.

## Installation

Install the plugin globally using the Antigravity Command-Line Interface (CLI):

```bash
agy plugin install https://github.com/AndyAWD/antigravity-doc-template
```

## Key Features

1. **Standardized Bilingual Layout**: Generates clean and symmetrical `README.md` (English) and `README.zh-TW.md` (Traditional Chinese) files with seamless reciprocal navigation links.
2. **One-Click Command Copying**: Strictly separates every CLI command and slash command into isolated code blocks, enabling users to click GitHub's copy button directly.
3. **Automated Metadata Extraction**: Intelligently analyzes `plugin.json`, `package.json`, and `skills/` directories in any plugin project to generate complete documentation without manual drafting.
4. **Structured Architecture Showcase**: Features ASCII directory tree diagrams accompanied by detailed component descriptions.
5. **Cross-Platform Ready**: Fully verified and compatible with CLI terminals, IDE sidebars, and Antigravity 2.0 chat environments.

## Plugin Management

• List installed plugins:

  ```bash
  agy plugin list
  ```

• Enable this plugin:

  ```bash
  agy plugin enable antigravity-doc-template
  ```

• Disable this plugin:

  ```bash
  agy plugin disable antigravity-doc-template
  ```

• Uninstall this plugin:

  ```bash
  agy plugin uninstall antigravity-doc-template
  ```

## Directory Structure

```text
antigravity-doc-template/
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
├── plugin.json
├── package.json
├── LICENSE
├── README.md
├── README.zh-TW.md
├── templates/
│   ├── README.template.md
│   ├── README.zh-TW.template.md
│   ├── RELEASE.template.md
│   ├── PULL_REQUEST_TEMPLATE.md
│   ├── PULL_REQUEST_TEMPLATE.en.md
│   └── PULL_REQUEST_TEMPLATE.bilingual.md
└── skills/
    ├── sync-readme/
    │   └── SKILL.md
    ├── agy-doc-release/
    │   └── SKILL.md
    └── agy-doc-github-pr/
        └── SKILL.md
```

## Commands and Skills

Once installed, trigger capabilities using natural language prompts or dedicated slash commands:

### 1. Bilingual Documentation Sync (sync-readme)

```text
/antigravity-doc-template:sync-readme
```

- **When to Use**: When creating, updating, or refactoring bilingual README files.
- **How It Works**:
  1. Inspects workspace structure, manifests, and `skills/` directory.
  2. Automatically identifies execution mode (Create, Update, or Refactor).
  3. Synchronizes symmetric `README.md` (English) and `README.zh-TW.md` (Traditional Chinese) adhering to standard specifications.

### 2. Bilingual GitHub Release Notes Generator (agy-doc-release)

```text
/antigravity-doc-template:agy-doc-release
```

- **When to Use**: When cutting a new version release, tagging a milestone, or creating a formal GitHub Release.
- **How It Works**:
  1. Inspects the previous Git tag and calculates the commit range (`git log <prev-tag>..HEAD`).
  2. Categorizes commits according to Conventional Commits (Feat, Fix, Refactor, Perf, Style, Test, Docs, Chore).
  3. Generates bilingual release notes featuring dual sections (`English` & `繁體中文`), author attribution, and full changelog comparison links.
  4. Optionally publishes the release directly via GitHub CLI (`gh release create`).

### 3. GitHub Pull Request Description Generator (agy-doc-github-pr)

```text
/antigravity-doc-template:agy-doc-github-pr
```

- **When to Use**: When preparing to submit a Pull Request, initiating code review, or publishing feature/fix branches.
- **How It Works**:
  1. Inspects branch status and verifies remote tracking against main.
  2. **Interactively prompts user for preferred PR language via `ask_question`** (Traditional Chinese, English, or Bilingual Parallel).
  3. Analyzes branch diffs and synthesizes purpose, summaries, and automatically checks types and affected components in the chosen language.
  4. Formulates verification steps, test results, and pre-submission checklists.
  5. Optionally creates the formal PR directly via GitHub CLI (`gh pr create`).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
