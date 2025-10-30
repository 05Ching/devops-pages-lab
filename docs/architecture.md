# DevOps Pages Lab – Workflow Architecture

## Overview
This repository automates the process of updating and deploying a GitHub Pages site using GitHub Actions.

## Workflow Pipeline
1. **Trigger**
   - Runs daily at 06:00 (Taipei Time, 22:00 UTC).
   - Can also be triggered manually via “Run workflow” in Actions.

2. **Fetch Stage**
   - The workflow retrieves the latest 20 public GitHub events from my account using the GitHub REST API.

3. **Transform Stage**
   - Extracts event types, repositories, and timestamps, formats them into Markdown.

4. **Inject Stage**
   - Replaces content between the placeholders in `README.md`:
     ```
     <!--ACTIVITY-LOG:START-->
     <!--ACTIVITY-LOG:END-->
     ```
   - Commits the updated README.

5. **Deploy Stage**
   - GitHub Pages automatically rebuilds the site, rendering `index.md` which includes `README.md`.

## Schedule Rationale
Daily updates at 06:00 align with the end of my typical working day and minimize API rate-limit risks.

## Security Notes
- The workflow uses a Personal Access Token stored securely as `TOKEN` under repo secrets.
- The workflow has minimum permission: `contents: write`.

## Repo Hygiene
- `.github/workflows/` for automation YAML.
- `docs/` for documentation.
- `index.md` for homepage rendering.
- `README.md` for content source.

---

_This documentation demonstrates a complete CI/CD pipeline for a static site, integrating automation, visibility, and security._
