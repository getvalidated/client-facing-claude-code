## Session Start
On the first message of any new session:
1. Run `git pull origin main` to update the repository
2. Read the `install_version` from the top of `INSTALL.md` (look for `<!-- version: X.X -->`)
3. Check `~/.claude/.install-status` — a JSON file tracking completed setup steps
   - If the file **does not exist**, read `INSTALL.md` and run all steps
   - If the file exists but its `"version"` field **does not match** `INSTALL.md`'s version, **delete the file** and re-run all steps from `INSTALL.md`
   - If the version matches and **all steps** are marked `true`, skip INSTALL.md entirely
   - If the version matches but **any step** is `false`, read `INSTALL.md` and run only the incomplete steps
   - After completing each step, update the status file:
     ```bash
     python3 -c "import json,pathlib;p=pathlib.Path.home()/'.claude'/'.install-status';d=json.loads(p.read_text()) if p.exists() else {};d['STEP_KEY']=True;p.write_text(json.dumps(d,indent=2))"
     ```
4. Only then proceed with the user's request

## Projects Directory
Related project repositories are cloned to `~/projects/`:
- `~/projects/AutomatedBasicEditing` — The AutomatedBasicEditing web terminal application (frontend + backend)
- `~/projects/client-facing-claude-code` — This repository

### User Project Organization
When creating deliverables for a user (reports, scripts, analyses), organize output into:
```
~/projects/{company}-{task}-{date}/
```
For example: `~/projects/acme-performance-report-2026-02-13/`

After saving files, guide the user: **click the Files action in the toolbar** > navigate to the project folder > click **preview** on any `.html` file to view it in-browser.

## Uploads Directory
User-uploaded files are stored at `~/uploads/`. Users can upload files (up to 500MB) using the **Upload** action in the toolbar.

## GUI Interface
The toolbar at the bottom of the chat provides these actions:

| Action | What it does |
|--------|-------------|
| **MCP Auth** | Authenticate or re-authenticate MCP server connections (Valid, Linear, etc.) |
| **Control Keys** | Open a reference of keyboard shortcuts for the terminal |
| **Resume** | Resume the most recent interrupted Claude Code session |
| **Files** | Browse the workspace file tree — navigate folders, click files to view, click **preview** on HTML files to open them in-browser |
| **Upload** | Upload files from your device into `~/uploads/` (max 5 GB) |
| **Clear** | Clear the current terminal display (does not erase conversation history) |
| **Logs** | View Claude Code system logs for debugging |

### Showing results to users
When you generate an HTML file (report, dashboard, visualization):
1. Save it to the appropriate project directory
2. Tell the user: *"Click **Files** in the toolbar, navigate to `{path}`, and click **preview** on the `.html` file to view it."*
