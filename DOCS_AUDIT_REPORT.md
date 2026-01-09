# Chucky Documentation Audit Report

## Executive Summary

After reviewing the CLI, SDK, and landing page, I've identified several gaps between what the platform offers and what's documented. The documentation is technically accurate but doesn't fully capture Chucky's unique value proposition or guide users through the most compelling workflows.

---

## Platform Overview (Current Understanding)

**Chucky = "The Vercel for AI Agents"**

Core differentiators:
1. **Built-in per-user billing** - JWT tokens with embedded budgets, enforced at the edge
2. **Possession Mode** - Cloud reasoning + local tool execution
3. **Browser + Server tools** - Same SDK works in both environments
4. **Background jobs + cron** - Fire-and-forget task execution
5. **Git bundle workflow** - Sync agent changes back to local repos

---

## Documentation Gaps

### 1. Missing: "Why Chucky?" / Value Proposition Page

**Problem**: The intro page (`index.mdx`) describes *what* Chucky does but not *why* someone would choose it over alternatives (direct Anthropic API, OpenAI, etc.).

**Recommendation**: Add a "Why Chucky?" page that covers:
- The billing problem Chucky solves (AI cost explosion for SaaS)
- Comparison: Direct API vs Chucky
- The "without vs with" messaging from the landing page
- Target use cases (agencies billing clients, SaaS teams, indie devs)

---

### 2. Missing: Architecture / How It Works Page

**Problem**: No visual explanation of the system architecture. Users don't understand the flow: Browser → Chucky Cloud → Claude API.

**Recommendation**: Add an architecture page with:
- System diagram (matching landing page)
- Explanation of the sandbox environment
- How tools execute (client-side vs server-side)
- How possession mode works (cloud brain, local hands)

---

### 3. Incomplete: Deployment / Workspace Documentation

**Problem**: `advanced/workspace.mdx` exists but the CLI has extensive deployment features not fully documented:
- `chucky deploy` workflow
- `.chucky.json` configuration schema
- `.chucky` binding file (git-ignored)
- Workspace archive creation and R2 upload
- GitHub Actions integration

**Recommendation**: Expand workspace docs to cover:
- Complete `.chucky.json` schema with all options
- Deployment workflow step-by-step
- CI/CD integration (GitHub Actions template is auto-generated)
- Environment variables (`CHUCKY_API_KEY`, `CHUCKY_PORTAL_URL`, `CHUCKY_WORKER_URL`)

---

### 4. Missing: Possession Mode Deep Dive

**Problem**: `cli/possession.mdx` likely exists but the feature deserves more prominence. This is a unique Chucky capability.

**Recommendation**: Ensure possession mode docs cover:
- Concept explanation (cloud reasoning, local execution)
- All 6 host tools: `HostBash`, `HostRead`, `HostWrite`, `HostEdit`, `HostGlob`, `HostGrep`
- Security considerations
- Use cases (IDE integrations, local agents, desktop apps)
- System prompt auto-injection for possession context

---

### 5. Incomplete: API Reference

**Problem**: `api/rest.mdx`, `api/websocket.mdx`, `api/incubate.mdx` exist but may not cover all endpoints.

**Recommendation**: Verify these endpoints are documented:
- `/incubate` - Job creation (REST)
- `/ws` - WebSocket connection
- Portal API endpoints (projects, sessions, jobs, bundles)
- Webhook callback format and HMAC signature verification

---

### 6. Missing: Complete SDK Options Reference

**Problem**: The SDK has many session options not fully documented:
- `forkSession`, `resumeSessionAt`, `continue`
- `agents` (sub-agent definitions)
- `permissionMode`, `allowDangerouslySkipPermissions`
- `env` (environment variables)
- `outputFormat` with JSON schema
- `maxThinkingTokens`
- `fallbackModel`

**Recommendation**: Add comprehensive options reference showing all `SessionOptions` with examples.

---

### 7. Missing: Use Cases / Recipes Section

**Problem**: No practical guides showing end-to-end workflows for the use cases highlighted on the landing page.

**Recommendation**: Add use case guides:
1. **Building an AI-Powered CLI Tool** - Using possession mode
2. **Creating a Browser Extension with Claude** - Browser tools + DOM manipulation
3. **White-Label AI Platform** - Per-user billing setup, token generation endpoint
4. **CI/CD Integration** - GitHub Actions for PR reviews, changelog generation
5. **Scheduled Automation** - Cron jobs for nightly audits

---

### 8. Incomplete: CLI Command Reference

**Problem**: New commands added but may need polish:
- `chucky wait` (wait for job completion)
- `chucky sessions get` (individual session details)
- Partial ID resolution (git-style prefix matching)

**Recommendation**: Add to CLI docs:
- Complete `chucky wait` documentation
- Session detail viewing
- Explain partial ID resolution for sessions/jobs
- Exit codes reference (0=SUCCESS, 1=CONFLICT, etc.)

---

### 9. Missing: Error Handling Best Practices

**Problem**: `advanced/error-handling.mdx` exists but may not cover all SDK error types.

**Recommendation**: Ensure coverage of:
- All error classes: `ConnectionError`, `AuthenticationError`, `BudgetExceededError`, `ConcurrencyLimitError`, `RateLimitError`, `SessionError`, `ToolExecutionError`, `TimeoutError`, `ValidationError`
- How to handle each error type
- Retry strategies
- Budget exceeded recovery patterns

---

### 10. Missing: MCP Server Types

**Problem**: SDK supports multiple MCP server types but docs focus mainly on client-side tools.

**Recommendation**: Document all MCP server types:
- Client-side tools (with handlers) - Current focus
- Stdio servers (external processes)
- SSE servers (Server-Sent Events endpoints)
- HTTP servers (REST API endpoints)

---

### 11. Outdated/Missing: Python, Go, PHP SDK Docs

**Problem**: These SDKs are listed but may not be fully implemented or documented.

**Recommendation**:
- Audit each SDK's actual implementation status
- Update docs to reflect what's actually available
- If SDKs are partial/planned, clearly mark as "Coming Soon"

---

### 12. Missing: Pricing / Billing Documentation

**Problem**: No docs explaining:
- Pricing tiers (Hobby $5, Starter $29, Pro $99)
- What counts as compute vs AI cost
- How budgets are tracked and enforced
- Overage pricing

**Recommendation**: Add billing guide covering:
- Pricing breakdown
- Understanding your bill
- Budget window behavior (hour/day/week/month)
- Monitoring usage in the portal

---

## Information Architecture Recommendations

### Current Structure:
```
Guides/
├── Getting Started
├── Core Concepts
├── CLI
└── Advanced
```

### Recommended Structure:
```
Guides/
├── Getting Started
│   ├── Introduction
│   ├── Why Chucky?        # NEW
│   ├── Quickstart
│   └── Authentication
├── Core Concepts
│   ├── Architecture       # NEW (expanded)
│   ├── Sessions
│   ├── Tools
│   ├── Streaming
│   └── MCP Servers        # NEW
├── CLI
│   ├── Overview
│   ├── Prompt Command
│   ├── Jobs
│   ├── Git Bundles
│   ├── Sessions
│   ├── Possession Mode
│   ├── Cron Jobs
│   └── Deployment         # NEW (expanded)
├── Use Cases              # NEW section
│   ├── AI CLI Tools
│   ├── Browser Extensions
│   ├── White-Label Platform
│   ├── CI/CD Integration
│   └── Scheduled Automation
└── Advanced
    ├── Error Handling
    ├── Budget Management
    ├── Workspace Configuration
    └── Billing & Pricing   # NEW
```

---

## Priority Fixes

### High Priority (Blocking user adoption):
1. **Add "Why Chucky?" page** - Essential for conversion
2. **Complete deployment docs** - Users can't deploy without this
3. **Add architecture page** - Users confused about how it works

### Medium Priority (Improving experience):
4. **Use case guides** - Show practical applications
5. **Complete SDK options reference** - Power users need this
6. **Possession mode deep dive** - Unique feature deserves prominence

### Low Priority (Polish):
7. **Error handling best practices** - Improve developer experience
8. **MCP server types** - Advanced feature documentation
9. **Billing documentation** - Business-critical but can wait

---

## Consistency Issues

### Naming Inconsistencies:
- Landing page says "Possession Mode", docs should use consistently
- "Host tools" vs "Host Tools" vs "HostBash" - standardize capitalization
- "MCP servers" vs "mcpServers" vs "MCP Servers"

### Code Example Issues:
- Some examples use `client.prompt()`, others use `session.send()` - clarify when to use each
- Go/PHP examples in quickstart are verbose - consider simplifying
- Missing error handling in most examples

### Navigation Issues:
- CLI section doesn't link to API reference (they're related)
- No cross-linking between concepts and CLI commands that implement them

---

## Landing Page → Docs Alignment

The landing page promises:

| Landing Page Claim | Docs Coverage |
|-------------------|---------------|
| "Per-user billing enforcement" | Partial (authentication.mdx) |
| "Possession Mode" | Exists but needs expansion |
| "Browser + Server tools" | Partial (tools.mdx) |
| "MCP servers & custom tools" | Partial |
| "Multi-turn sessions" | Good (sessions.mdx) |
| "Streaming responses" | Good (streaming.mdx) |
| "Full file & shell access" | Not explicitly documented |
| "Background jobs & cron" | Good (jobs.mdx, cron.mdx) |

---

## Recommended Action Items

1. [ ] Create "Why Chucky?" page
2. [ ] Create architecture/how-it-works page
3. [ ] Expand workspace/deployment documentation
4. [ ] Create use case guides (start with 2-3)
5. [ ] Add complete SDK options reference
6. [ ] Document all MCP server types
7. [ ] Add billing/pricing documentation
8. [ ] Standardize naming conventions
9. [ ] Add cross-links between related pages
10. [ ] Review and update Python/Go/PHP SDK docs
