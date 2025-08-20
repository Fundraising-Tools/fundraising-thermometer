# Install Guide (Where files go)

Copy these files to your repository:

**Root (project base):**
- `README.md` (optional; provided in this bundle)
- `workflow_toggle_flowchart.png`
- `linkedin_toggle_cheatsheet.png`

**.github/workflows/**
- `build-thermometer.yml`
- `linkedin-preview.yml`
- `linkedin-publish-group-ready.yml`
- `linkedin-post-test-harness.yml`
- `linkedin-group-toggle.yml`
- `linkedin-post-template.md`
- `README-workflows.md` (reference for contributors & maintainers)
- `ignore.txt` (optional — add to **disable** LinkedIn workflows; remove to enable)

After copying:
1. In GitHub → **Settings → Environments** → create environment **`linkedin`**.
2. Add secrets: `LINKEDIN_ACCESS_TOKEN`, `LINKEDIN_AUTHOR_URN` (optional `LINKEDIN_GROUP_URN`).
3. Add required reviewers to the `linkedin` environment for publish approval.
4. (Optional) Keep `.github/workflows/ignore.txt` present to suppress LinkedIn jobs on forks or until you’re ready.
5. To enable **Group messaging** in the template, comment `/group-on` in a PR. `/group-off` to go back.
