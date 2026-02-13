<!-- version: 1.0 -->

## Step 0 — Check Install Status

Before running any steps, read `~/.claude/.install-status`. This JSON file tracks which steps have been completed and includes a `"version"` field. **Skip any step where the key is `true`.** If the file does not exist, run all steps.

When writing or updating the status file, always include the version from the top of this file.

After completing each step, update the status file:
```bash
python3 -c "import json,pathlib;p=pathlib.Path.home()/'.claude'/'.install-status';d=json.loads(p.read_text()) if p.exists() else {};d['version']='1.0';d['STEP_KEY']=True;p.write_text(json.dumps(d,indent=2))"
```
Replace `STEP_KEY` with the key listed for that step.

---

## Step 1 — Git & GitHub CLI Setup
**Status key:** `git_github_cli`

- Check if git is installed, install if missing
- Check if gh CLI is installed, install if missing
- Check if gh is authenticated, if not guide me through login
- If I need a GitHub account, help me create one
- Avoid using Homebrew for this step if possible

---

## Step 2 — Clone Project Repository
**Status key:** `clone_repo`

- Clone to: `~/projects/client-facing-claude-code`
- Repo URL: `https://github.com/getvalidated/client-facing-claude-code.git`
- If `~/projects` doesn't exist, create it first
- If already cloned at that path, skip and confirm it exists
- This path will be used for the desktop launcher

---

## Step 3 — Create Desktop Launcher
**Status key:** `desktop_launcher`

Skip if already exists. Create a desktop file/shortcut that:
1. Changes directory to `~/projects/client-facing-claude-code`
2. Opens a terminal running `claude --dangerously-skip-permissions`

Add a cool icon to make it easy to find. Tell the user it's ready so they can use it to restart Claude if needed.

---

## Step 4 — Install Valid Brand Kit
**Status key:** `valid_brand_kit`

- Check the repo root and `~/Downloads` for `valid-brand.skill` (may have extra suffixes like `(1)`)
- If `~/.claude/skills` directory doesn't exist, create it
- Unzip and extract contents to `~/.claude/skills/valid-brand/` (skip if `SKILL.md` already exists there)
- Ensure `~/.claude/CLAUDE.md` contains the line: `When reading table data as a response from Valid generate a plot using matplotlib and reference the valid-brand skill`
- Ensure `~/.claude/CLAUDE.md` contains the following section (add it if not present):
  ```
  ## Session Management
  When context usage exceeds ~50k tokens, rename the session with `/rename {descriptive-name}` and inform the user.
  ```
- Only add lines/sections if they are not already present
- If the `.skill` file is not found, prompt the user to download it from Slack

---

## Step 5 — Install MCP Servers
**Status key:** `mcp_servers`

Skip any already configured:
- **Valid MCP:** `claude mcp add --transport http --scope user chat-with-your-ads https://v1.valid-gke-data-api.com/api/mcp/`
- **Linear MCP:** `claude mcp add --transport http linear-server https://mcp.linear.app/mcp`

---

## Step 6 — Install Context7 MCP
**Status key:** `context7_mcp`

```bash
claude mcp add --transport http --scope user context7 https://mcp.context7.com/mcp
```

---

## Step 7 — Install Valid Client Report Skill
**Status key:** `valid_client_report_skill`

- Look for `valid-client-report.skill` in the repo root (`~/projects/client-facing-claude-code/`)
- If `~/.claude/skills/valid-client-report/` doesn't exist, create it
- Unzip and extract contents: `unzip valid-client-report.skill -d ~/.claude/skills/`
- Verify `~/.claude/skills/valid-client-report/SKILL.md` exists
- If the `.skill` file is not found, run `git pull origin main` and retry

---

## Done

IMPORTANT: When all steps are complete, remind the user to **restart Claude Code** using the desktop launcher for all changes to take effect. Use the `/exit` command.

Please check what's already done before making changes, and let me know which steps were skipped vs completed.
