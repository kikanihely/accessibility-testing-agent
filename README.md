<h1 align="center">♿ Accessibility Testing Agent</h1>
 
<p align="center">
  <em>Give it a URL. It audits the live page. Saves a Word report. Automatically.</em>
</p>
<p align="center">
  <img src="https://img.shields.io/badge/WCAG%202.1%20AA-0052CC?style=for-the-badge&logoColor=white" />
  <img src="https://img.shields.io/badge/Puppeteer%20MCP-40B5A4?style=for-the-badge&logo=puppeteer&logoColor=white" />
  <img src="https://img.shields.io/badge/axe--core%204.9.1-663399?style=for-the-badge&logoColor=white" />
  <img src="https://img.shields.io/badge/Claude%20AI-CC785C?style=for-the-badge&logoColor=white" />
  <img src="https://img.shields.io/badge/Filesystem%20MCP-2D2D2D?style=for-the-badge&logoColor=white" />
</p>
---
 
## 📌 What It Does
 
This is an AI-powered accessibility testing agent built with **Claude + MCP servers**. You give it any live website URL — it launches a real headless browser, runs a full WCAG 2.1 audit, checks keyboard navigation, and automatically saves a structured Word report to your Desktop.
 
No guessing. No static analysis. It tests the **live, rendered DOM** — exactly as a real user would experience it.
 
---
 
## ⚙️ How It Works
 
```
You give a URL
      ↓
Puppeteer MCP launches real headless Chromium browser
      ↓
axe-core injected → full WCAG 2.1 AA audit runs on live DOM
      ↓
Keyboard navigation simulated (Tab order, focus traps, skip links)
      ↓
Violations grouped by WCAG principle
      ↓
Filesystem MCP saves complete .docx report to Desktop
```
 
---
 
## 🛠️ MCP Servers Used
 
| MCP Server | Purpose |
|---|---|
| [Puppeteer MCP](https://www.npmjs.com/package/@modelcontextprotocol/server-puppeteer) | Launches real headless Chromium, navigates URLs, injects axe-core, simulates keyboard |
| [Filesystem MCP](https://www.npmjs.com/package/@modelcontextprotocol/server-filesystem) | Writes the final `.docx` audit report to your Desktop |
 
---
 
## 🧪 What Gets Tested
 
### WCAG 2.1 Principles Covered
| Principle | What It Checks |
|---|---|
| **Perceivable** | Alt text, color contrast (4.5:1), info structure, error messages |
| **Operable** | Keyboard access, focus order, focus visibility, skip links |
| **Understandable** | Form labels, error identification, field descriptions |
| **Robust** | Semantic HTML, ARIA roles, name/role/value on interactive elements |
 
### Keyboard Navigation
- Tab order logic
- Focus trap detection in modals
- Focus visibility on all interactive elements
- Skip to main content link presence
### Impact Levels
| Level | Color | Meaning |
|---|---|---|
| Critical | 🔴 | Blocks task completion entirely |
| Serious | 🟠 | Severely degrades the experience |
| Moderate | 🟡 | Makes tasks harder but not impossible |
| Minor | 🟢 | Small friction for affected users |
 
---
 
## 💬 How to Use
 
Set up Claude Desktop with both MCP servers, paste the prompt from `prompts/`, then simply type:
 
```
Test https://example.com for accessibility
```
 
**Other supported input formats:**
```
Audit https://example.com for WCAG 2.1 AA only
Test the checkout flow at https://shop.com/cart
Check only form accessibility on https://example.com/contact
Test https://example.com on mobile viewport (375px)
```
 
**Defaults (if not specified):**
- WCAG Level: 2.1 AA
- Viewport: Desktop 1280 x 800
- Scope: Full page audit
---
 
## 📄 Output
 
### In Chat — Audit Summary
```
URL:            https://example.com
Audited:        2025-05-26
Viewport:       1280 x 800
WCAG Level:     2.1 AA
Violations:     9
Passes:         47
Manual Review:  4
 
4 Critical / 3 Serious / 2 Moderate / 0 Minor | Passes: 47 | Manual review: 4
```
 
### Violation Table (per WCAG principle)
```
ID       | WCAG Rule              | Element           | Impact   | Affected Users          | Fix
A11Y-001 | 1.1.1 Non-text content | <img src="...">   | Critical | Blind / screen reader   | Add alt attribute
A11Y-002 | 1.4.3 Contrast         | .btn-primary      | Serious  | Low-vision users        | Change color to #595959
```
 
### Fix Priority Queue
Top 5 violations ranked by impact + frequency — so developers know exactly what to fix first.
 
### Word Report (auto-saved)
```
📄 Full report saved to Desktop: a11y-audit-example-com-2025-05-26.docx
```
 
The `.docx` report includes:
- Cover page with audit metadata
- Summary scorecard table
- Violations by WCAG principle (color-coded by impact)
- Keyboard navigation findings table
- Manual review checklist
- Fix Priority Queue (top 5)
---
 
## 🗂️ Repo Structure
 
```
accessibility-testing-agent/
├── README.md
├── prompts/
│   └── accessibility-testing-agent-prompt.md   ← paste this into Claude Desktop
└── sample-output/
    └── sample-audit-report.md                  ← example audit result
```
 
---
 
## 🚀 Setup
 
### Prerequisites
- [Claude Desktop](https://claude.ai/download) installed
- Node.js installed (for MCP servers)
### Install MCP Servers
```bash
npm install -g @modelcontextprotocol/server-puppeteer
npm install -g @modelcontextprotocol/server-filesystem
```
 
### Configure Claude Desktop
Add both servers to your `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "puppeteer": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-puppeteer"]
    },
    "filesystem": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-filesystem", "/Users/YOUR_USERNAME/Desktop"]
    }
  }
}
```
 
### Use the Agent
1. Open Claude Desktop
2. Paste the contents of `prompts/accessibility-testing-agent-prompt.md` as the system prompt
3. Type a URL and hit enter
---
 
## 📚 What I Learned Building This
 
- How WCAG 2.1 principles map to real user impact
- How axe-core detects violations on a live rendered DOM vs static HTML
- How to chain MCP servers (Puppeteer → audit → Filesystem → report)
- Keyboard navigation patterns — focus traps, tab order, skip links
- How to structure AI agent prompts for multi-step testing workflows
---
 
## 🙋 Author
 
**Kikani Hely**
