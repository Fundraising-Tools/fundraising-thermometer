# Workflows Guide

## Directory Layout
- **/.github/workflows/**
  - `build-thermometer.yml`
  - `linkedin-preview.yml`
  - `linkedin-publish-group-ready.yml`
  - `linkedin-post-test-harness.yml`
  - `linkedin-group-toggle.yml`
  - `linkedin-post-template.md`
  - `README-workflows.md` (this file)
  - `ignore.txt` (optional toggle)
  - `GROUP_MODE` (auto-created/removed by `/group-on` and `/group-off`)
- **/** (repo root)
  - `README.md` (short overview)
  - `workflow_toggle_flowchart.png`
  - `linkedin_toggle_cheatsheet.png`

## Secrets & Environment
Create an **environment** named `linkedin` and add secrets:
- `LINKEDIN_ACCESS_TOKEN`
- `LINKEDIN_AUTHOR_URN`
- (Optional) `LINKEDIN_GROUP_URN` if you use a private group

Protect the environment with required reviewers so posts are approved before publishing.

## ignore.txt Toggle
- Add `.github/workflows/ignore.txt` → LinkedIn workflows skip.
- Remove it → LinkedIn workflows run.

## ChatOps Toggle for Group Mode
- In a PR: `/group-on` → creates `.github/workflows/GROUP_MODE`
- In a PR: `/group-off` → removes it
- The publish job reads it via `hashFiles('.github/workflows/GROUP_MODE')` and sets `IF_GROUP` for your template’s conditional block.

## LinkedIn Template
Placeholders: `{{PR_TITLE}}`, `{{PR_NUMBER}}`, `{{PR_URL}}`, `{{REPO}}`, `{{REPO_URL}}`, `{{BASE_REF}}`, `{{MERGED_BY}}`, `{{AUTHOR}}`, `{{COMMIT_SHA}}`, `{{COMMIT_SHA_SHORT}}`, `{{LINK_URL}}`, `{{LINK_TITLE}}`, `{{IMAGE_URL}}`

Conditionals: `{{#IF_LINK}}...{{/IF_LINK}}`, `{{#IF_IMAGE}}...{{/IF_IMAGE}}`, `{{#IF_GROUP}}...{{/IF_GROUP}}`

## Approval & Safety
- Only OWNER/MEMBER/COLLABORATOR can invoke `/publish`, `/dry-run`, `/cancel`, `/group-on`, `/group-off`.
- Publish job requires approval via the `linkedin` environment.
- Secrets are masked in logs.
- Retries with backoff on `429/5xx`.

## Troubleshooting
- See the job Summary for **status (✅/❌)**, timestamp, links, **payload preview**, and **response snippet**.
- If preview/publish doesn’t run, check for `ignore.txt` or missing env approvals.
