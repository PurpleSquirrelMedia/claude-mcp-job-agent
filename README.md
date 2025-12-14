# Claude MCP Job Agent

> Using Claude to apply for a job at Anthropic - the ultimate meta demonstration.

An agentic job application system built with [Claude Code](https://claude.ai/claude-code) and [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) integrations. The system enables Claude to autonomously navigate job application websites, fill out forms, retrieve verification codes from email, and submit applications - all orchestrated through natural language conversation.

## The Meta Twist

This project demonstrates advanced Claude capabilities by using Claude itself to apply for a position at Anthropic. It's a practical showcase of:

- **Advanced Prompt Engineering** - Multi-tool orchestration across browser and email contexts
- **MCP Integration** - Real-world implementation of Model Context Protocol
- **Agentic Workflows** - Planning, executing, and adapting to different job site formats
- **Production Patterns** - OAuth2 auth, error handling, multi-step reasoning

## Architecture

```
Claude Code (Opus 4.5)
         │
         ├──▶ Playwright MCP
         │    ├── Browser automation
         │    ├── Form filling
         │    ├── File uploads
         │    └── Screenshot capture
         │
         ├──▶ Gmail MCP
         │    ├── OAuth2 authentication
         │    ├── Search emails
         │    └── Read verification codes
         │
         └──▶ Local Filesystem
              ├── Resumes (PDF/MD)
              ├── Cover letters
              └── Configuration
```

## How It Works

### 1. Start the conversation

```
User: "Apply to the Prompt Engineer role at Anthropic"
```

### 2. Claude takes over

1. **Navigate** - Opens Anthropic careers page via Playwright MCP
2. **Find** - Locates the relevant job posting
3. **Fill** - Reads your resume and maps content to form fields
4. **Upload** - Attaches resume PDF via file upload
5. **Verify** - If email verification needed, queries Gmail MCP
6. **Submit** - Completes the application

### 3. Zero manual intervention

No copy-pasting verification codes. No switching between tabs. Claude handles the entire flow.

## Setup

### Prerequisites

- [Claude Code CLI](https://claude.ai/claude-code) installed
- Node.js 18+
- Google Cloud project (for Gmail OAuth)

### 1. Configure MCP Servers

Create `~/.mcp.json`:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@playwright/mcp@latest"]
    }
  }
}
```

### 2. Add Gmail MCP (for verification codes)

```bash
# Run the Gmail MCP auth flow
npx @gongrzhe/server-gmail-autoauth-mcp

# Add to Claude Code
claude mcp add gmail -s user -- npx @gongrzhe/server-gmail-autoauth-mcp
```

### 3. Prepare your documents

Place your resume and cover letters in a known location:

```
~/Documents/
├── Resume.pdf
├── Resume.md
└── CoverLetter_Anthropic.md
```

### 4. Apply!

```bash
claude
> "Apply to the Prompt Engineer position at Anthropic using my resume"
```

## Key Features

### Browser Automation

Playwright MCP provides full browser control:
- Navigate to any URL
- Click buttons and links
- Fill form fields
- Upload files
- Take screenshots for debugging

### Email Integration

Gmail MCP with OAuth2:
- Search inbox for specific emails
- Read email content
- Extract verification codes automatically
- Zero manual copy-paste

### Intelligent Form Mapping

Claude reads your resume/documents and:
- Identifies relevant sections
- Maps content to form fields
- Handles various form layouts
- Adapts to different job site formats

## Example Session

```
User: Apply to Anthropic's Cross-functional Prompt Engineer role

Claude: I'll help you apply. Let me:
1. Navigate to Anthropic's careers page
2. Find the Prompt Engineer position
3. Fill out the application using your resume

[playwright - Navigate to URL]
→ https://www.anthropic.com/careers

[playwright - Click]
→ "Cross-functional Prompt Engineer"

[playwright - Fill form]
→ Name: Matthew Karsten
→ Email: example@email.com
→ LinkedIn: linkedin.com/in/matthewkarsten

[playwright - Upload file]
→ Resume.pdf uploaded

[gmail - Search emails]
→ Found verification code: 847291

[playwright - Submit]
→ Application submitted successfully!
```

## Why This Matters

This isn't just a clever demo - it's a glimpse of where AI-assisted workflows are heading:

1. **Reduced Friction** - Tedious multi-step processes become single conversations
2. **Context Awareness** - AI that understands your documents and goals
3. **Tool Orchestration** - Multiple capabilities combined intelligently
4. **Human in the Loop** - You stay in control while AI handles the mechanics

## Files

- `index.html` - GitHub Pages demo site
- `README.md` - This file
- `~/.mcp.json` - MCP server configuration
- `~/.claude.json` - Claude Code settings

## Built With

- [Claude Code](https://claude.ai/claude-code) - AI coding assistant
- [Model Context Protocol](https://modelcontextprotocol.io/) - Tool integration standard
- [Playwright MCP](https://github.com/anthropics/mcp-server-playwright) - Browser automation
- [Gmail MCP](https://github.com/gongrzhe/server-gmail-autoauth-mcp) - Email integration

## Author

**Matthew Karsten** - [GitHub](https://github.com/ExpertVagabond) | [LinkedIn](https://www.linkedin.com/in/matthewkarsten/)

---

*Applying AI to get a job building AI*
