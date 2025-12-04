# Claude Code Project Setup Guide

## How Claude Code Auto-Reads Instructions

Claude Code automatically reads the `CLAUDE.md` file when you open a project. This is the **key file** that makes everything work without mentioning guidelines in prompts.

---

## Setup Instructions

### Step 1: Create Folder Structure

In your WordPress plugin/theme project root, create this structure:

```
your-project/
├── .claude/
│   ├── CLAUDE.md              ← AUTO-READ by Claude Code
│   ├── settings.json          ← Optional project settings
│   └── docs/                   ← Your guideline files
│       ├── claude_rules.md
│       ├── WordPress-Plugin-Submission-Complete-Guide.md
│       └── codecanyon-plugin-submission-guide.md
├── your-plugin-folder/
│   └── ... plugin files ...
```

### Step 2: Copy Files

1. Copy the `.claude` folder from this package to your project root
2. Or manually create the structure and copy these files:
   - `CLAUDE.md` → `.claude/CLAUDE.md`
   - `claude_rules.md` → `.claude/docs/claude_rules.md`
   - `WordPress-Plugin-Submission-Complete-Guide.md` → `.claude/docs/WordPress-Plugin-Submission-Complete-Guide.md`
   - `codecanyon-plugin-submission-guide.md` → `.claude/docs/codecanyon-plugin-submission-guide.md`

### Step 3: Alternative - Project Root CLAUDE.md

You can also place `CLAUDE.md` directly in project root (not inside .claude folder):

```
your-project/
├── CLAUDE.md                   ← Also works here!
├── .claude/
│   └── docs/
│       └── ... guideline files ...
```

---

## How It Works

1. **You open project in Claude Code**
2. **Claude Code automatically reads `CLAUDE.md`**
3. **All instructions are loaded without prompting**
4. **Every code generation follows the guidelines**

---

## Quick Commands (After Setup)

Just say these - Claude will follow all guidelines automatically:

| Command | What Happens |
|---------|--------------|
| "Create a WooCommerce plugin called X" | Full plugin structure with all security/standards |
| "Review this code for submission" | Checks against WP.org + CodeCanyon rules |
| "Fix the security issues" | Adds sanitization, escaping, nonces |
| "Make this CodeCanyon ready" | Full Envato compliance check |

---

## Verifying Setup Works

After setup, start Claude Code in your project and ask:

```
"What coding standards are you following for this project?"
```

Claude should reference WordPress coding standards, security requirements, and mention the guidelines from CLAUDE.md.

---

## Customizing for Specific Projects

Edit `CLAUDE.md` to add project-specific instructions:

```markdown
## Project-Specific Settings

- Plugin Name: SoroBindu AI Agent
- Text Domain: sorobindu-ai-agent
- Prefix: sorobindu_
- Minimum PHP: 8.0
- Minimum WP: 6.0
- Dependencies: WooCommerce 8.0+
```

---

## Folder Contents

```
claude-code-wp-setup/
├── .claude/
│   ├── CLAUDE.md                                    # Main auto-read file
│   ├── settings.json                                # Project settings
│   └── docs/
│       ├── claude_rules.md                          # General AI rules
│       ├── WordPress-Plugin-Submission-Complete-Guide.md  # WP.org guide
│       └── codecanyon-plugin-submission-guide.md    # CodeCanyon guide
└── README.md                                        # This file
```

---

## Tips

1. **Keep CLAUDE.md concise** - Put detailed docs in `/docs/` folder and reference them
2. **Update for each project** - Customize prefix, text-domain, dependencies
3. **Works with Git** - Commit `.claude/` folder to share with team
4. **Multiple projects** - Copy entire `.claude/` folder to each new project

---

## Support

For issues with Claude Code project instructions:
- Check file is named exactly `CLAUDE.md` (case-sensitive)
- Verify file is in project root or `.claude/` folder
- Restart Claude Code after adding files
