<p align="center">
  <img src="claude_animation.gif" alt="AI Job Search Assistant" width="200">
</p>

# AI Job Search

An AI-powered job application framework built on Claude Code. Fork it, fill in your profile, and use the workflow to evaluate job postings, tailor your CV, write cover letters, and prepare for interviews.

> Note: This is an independent open-source project and is not affiliated with, endorsed by, sponsored by, or maintained by Anthropic. Anthropic and Claude Code are referenced only to describe the toolchain this workflow uses.

## What this is

A structured workflow that turns Claude Code into a job application assistant. The core workflow is language- and country-agnostic. The included job-portal search skills target the Danish market, while the portal integration pattern can be adapted to other markets.

## Quick start

### 1. Fork and clone

```bash
gh repo fork MadsLorentzen/ai-job-search --clone
cd ai-job-search
```

### 2. Install job-search tools

```bash
cd .agents/skills/jobbank-search/cli && bun install && cd ../../../..
cd .agents/skills/jobdanmark-search/cli && bun install && cd ../../../..
cd .agents/skills/jobindex-search/cli && bun install && cd ../../../..
cd .agents/skills/jobnet-search/cli && bun install && cd ../../../..
cd .agents/skills/linkedin-search/cli && bun install && cd ../../../..
```

### 3. Set up your profile

```bash
claude
/setup
```

The setup workflow can import supported career documents or guide you through creating a profile.

### 4. Search and apply

```bash
/scrape
/apply https://example.com/job
```

If a job portal blocks automated access, provide the job description directly to `/apply` instead.

## Prerequisites

- Claude Code CLI
- Python 3.10+
- Bun for the included job-search CLI tools
- A LaTeX distribution with `lualatex` and `xelatex` for CV and cover-letter generation
- Optional: `pdftotext` from Poppler for ATS text-layer checks

## Main commands

- `/setup` - configure your profile and workflow
- `/scrape` - search configured job portals
- `/rank` - rank scraped jobs against your profile
- `/apply <url>` - evaluate a posting and prepare application materials
- `/outcome` - record application outcomes
- `/expand` - enrich the profile from configured public sources
- `/upskill` - identify skill gaps and create a learning plan
- `/add-template` - register a custom LaTeX template
- `/add-portal` - add a job-portal integration
- `/reset` - reset profile or document data

## Project structure

```text
ai-job-search/
├── CLAUDE.md
├── .claude/
│   ├── commands/       # Slash-command workflows
│   └── skills/         # Core application and job-search skills
├── .agents/skills/     # Job-portal CLI integrations
├── cv/                 # CV templates
├── cover_letters/      # Cover-letter templates and fonts
├── templates/          # User-registered templates
├── documents/          # Local career source material
├── job_scraper/        # Scraper state and results
├── upskill/            # Generated skill-gap reports
├── salary_lookup.py    # Salary benchmarking tool
├── tools/              # Supporting utilities
├── job_search_tracker.csv
└── SETUP.md
```

## Configuration

When editing the repository manually, update the profile and workflow guidance in `.claude/skills/job-application-assistant/` and `CLAUDE.md`.

Job-search configuration is handled through `/setup --section search`. Do not rely on a `search-queries.md` file unless your fork or custom configuration creates one.

## Application verification

The `/apply` workflow evaluates job fit, drafts application materials, runs a reviewer pass, compiles the generated PDFs, and performs ATS-oriented text extraction when `pdftotext` is available. Claims in application materials are intended to remain grounded in the candidate profile rather than fabricated.

## Custom templates and portals

Use `/add-template` to register a custom CV or cover-letter template. Use `/add-portal` to generate a search skill for another job board. Both workflows are designed to preserve the project's existing structure while allowing local customization.

## License

See the repository license for terms of use.
