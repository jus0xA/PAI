# PAI Deployment Guide for Claude Subscription

**Version:** Streamlined for Claude Code (no voice, no external APIs)

This guide will help you deploy PAI's world-class workflow routing and agent orchestration to your Claude Code setup.

---

## What You're Getting

**6 Production Agents:**
- `architect` - System design, PRDs, technical specifications
- `engineer` - Implementation, testing, optimization
- `designer` - UX/UI design, design systems
- `pentester` - Security testing, vulnerability assessment
- `researcher` - Research orchestration (spawns claude-researcher agents)
- `claude-researcher` - WebSearch-based research specialist

**9 Specialized Skills:**
- `CORE` - System identity, routing, orchestration patterns
- `research` - Multi-perspective research with parallel agents
- `prompting` - Prompt engineering best practices
- `fabric` - 242+ content processing patterns
- `alex-hormozi-pitch` - Business offer creation
- `system-createcli` - TypeScript CLI generation
- `system-createskill` - Skill creation framework
- `create-skill` - Skill templates
- `ffuf` - Web fuzzing guidance

**Key Features:**
- ✅ No external APIs required (uses Claude's built-in WebSearch)
- ✅ No voice integration (streamlined for text)
- ✅ Sophisticated skill-based routing
- ✅ Multi-agent orchestration with Task tool
- ✅ Parallel execution for complex research
- ✅ Production-quality methodologies

---

## Prerequisites

- Claude Code CLI installed and working
- Access to Claude subscription (no API keys needed!)
- Your `.claude` folder location (usually `~/.claude`)

---

## Installation Steps

### Step 1: Locate Your .claude Folder

```bash
# On macOS/Linux
ls -la ~/.claude

# On Windows
dir %USERPROFILE%\.claude
```

If the folder doesn't exist, Claude Code will create it on first run.

### Step 2: Copy Skills and Agents

From this PAI repository, copy two directories to your `.claude` folder:

```bash
# Navigate to your .claude folder
cd ~/.claude

# Copy skills directory
cp -r /path/to/PAI/.claude/skills ./

# Copy agents directory
cp -r /path/to/PAI/.claude/agents ./
```

**Windows (PowerShell):**
```powershell
cd $env:USERPROFILE\.claude
Copy-Item -Path "C:\path\to\PAI\.claude\skills" -Destination .\ -Recurse
Copy-Item -Path "C:\path\to\PAI\.claude\agents" -Destination .\ -Recurse
```

### Step 3: Verify Installation

Check that files were copied correctly:

```bash
ls ~/.claude/skills/
# Should show: CORE, alex-hormozi-pitch, create-skill, fabric, ffuf, prompting, research, system-createcli, system-createskill

ls ~/.claude/agents/
# Should show: architect.md, claude-researcher.md, designer.md, engineer.md, pentester.md, researcher.md
```

### Step 4: (Optional) Set Up Fabric Skill

The fabric skill requires a one-time git clone:

```bash
cd ~/.claude/skills/fabric
git clone https://github.com/danielmiessler/fabric.git fabric-repo
```

This gives you access to 242+ specialized content processing patterns.

---

## How It Works

### Automatic Skill Routing

When you use Claude Code, PAI automatically routes your requests to the right skills and agents:

**Example 1: Research**
```
You: "Research the best React state management library for large-scale apps"

→ PAI activates research skill
→ Launches researcher agent
→ Researcher spawns 5 claude-researcher agents in parallel
→ Each researches a different perspective
→ Results synthesized in ~60 seconds
```

**Example 2: Feature Development**
```
You: "Build a user authentication system with JWT"

→ PAI launches architect agent
→ Architect creates comprehensive PRD
→ Then launches engineer agent
→ Engineer implements from PRD with tests
```

**Example 3: Design Work**
```
You: "Design a checkout flow with accessibility in mind"

→ PAI launches designer agent
→ Designer creates user-centered, accessible design
→ Provides implementation guidance
```

### Agent Orchestration

PAI uses Claude Code's Task tool to spawn specialized agents:

**Single Agent:**
- For focused, specialized tasks
- One perspective needed

**Multiple Agents (Parallel):**
- For complex multi-perspective work
- Independent tasks that can run simultaneously
- Research requiring diverse sources

**Sequential Agents:**
- For multi-stage workflows
- When one agent's output feeds the next
- Example: architect → engineer

---

## Testing Your Setup

### Test 1: Check CORE Skill Loaded

Start a new Claude Code session. The CORE skill should auto-load and Claude will understand PAI's routing patterns.

Ask: "What skills do you have available?"

Expected: Claude lists the 9 skills and explains their purposes.

### Test 2: Test Agent Launch

Ask: "Use the researcher agent to find the latest trends in AI agent orchestration"

Expected:
- Claude launches researcher agent via Task tool
- Researcher may spawn multiple claude-researcher agents
- Returns synthesized findings with sources

### Test 3: Test Multi-Agent Orchestration

Ask: "I want to build a REST API for a todo app. Help me design and implement it."

Expected:
- Claude launches architect agent first
- Architect creates PRD
- Then engineer agent implements
- You get comprehensive design + implementation

---

## Customization

### Personalizing CORE Skill

Edit `~/.claude/skills/CORE/SKILL.md` to customize:

1. **Identity Section** (lines 14-18)
   - Change the name from "PAI" to your preference
   - Adjust the role description

2. **Stack Preferences** (lines 104-118)
   - Modify language preferences
   - Add your preferred frameworks
   - Update tooling choices

3. **Agent Routing** (lines 49-102)
   - Add custom routing patterns
   - Modify when each agent activates

### Adding Your Own Skills

Use the `create-skill` or `system-createskill` skills to generate new skills:

```
You: "Create a new skill for Python data science workflows"

→ Claude uses system-createskill
→ Generates complete skill structure
→ Includes routing, documentation, examples
```

### Modifying Agent Personalities

Each agent file (`~/.claude/agents/*.md`) can be edited to adjust:
- Expertise focus areas
- Communication style
- Methodologies
- Quality standards

---

## Workflow Examples

### Example 1: Comprehensive Research

**Your Request:**
"Research the best database for a real-time analytics platform handling 1M+ events per second"

**PAI's Workflow:**
1. Activates research skill
2. Launches researcher agent
3. Researcher decomposes into 5 perspectives:
   - Performance benchmarks
   - Operational complexity
   - Cost analysis
   - Real-world case studies
   - Scaling patterns
4. Spawns 5 claude-researcher agents (parallel)
5. Each uses WebSearch for their perspective
6. Researcher synthesizes findings
7. Returns recommendation with confidence levels

**Time:** ~60 seconds

### Example 2: Full-Stack Feature

**Your Request:**
"Build a notification system with email, SMS, and push notifications"

**PAI's Workflow:**
1. Launches architect agent
2. Architect creates:
   - System architecture
   - API specification
   - Database schema
   - Integration points
   - Testing strategy
3. You review PRD
4. Launches engineer agent
5. Engineer implements:
   - Core notification service
   - Provider integrations
   - Queue management
   - Error handling
   - Tests

**Time:** ~5-10 minutes (depending on scope)

### Example 3: Security Audit

**Your Request:**
"Audit this API for security vulnerabilities"

**PAI's Workflow:**
1. Launches pentester agent
2. Pentester performs:
   - Input validation review
   - Authentication/authorization check
   - SQL injection testing
   - XSS vulnerability scan
   - Security header analysis
3. Returns comprehensive report
4. Provides remediation guidance

**Time:** ~2-5 minutes

---

## Troubleshooting

### Skills Not Loading

**Issue:** Claude doesn't seem to recognize skills

**Fix:**
- Verify files are in `~/.claude/skills/` (not a subfolder)
- Check file names match exactly (case-sensitive)
- Restart Claude Code session

### Agents Not Launching

**Issue:** Agent isn't spawning when requested

**Fix:**
- Verify files are in `~/.claude/agents/` directory
- Check YAML frontmatter is valid (name, description, model)
- Try explicitly: "Use the Task tool to launch the researcher agent"

### Fabric Skill Not Working

**Issue:** Fabric patterns not found

**Fix:**
```bash
cd ~/.claude/skills/fabric
git clone https://github.com/danielmiessler/fabric.git fabric-repo
```

### Research Agent Returns Empty

**Issue:** Research completes but no results

**Possible Causes:**
- WebSearch may be rate-limited (wait a moment and retry)
- Query too broad (make more specific)
- Network issues

**Fix:**
- Try a more specific research query
- Check internet connection
- Retry after a few seconds

---

## Advanced Usage

### Parallel Agent Execution

For maximum speed on independent tasks:

```
You: "In parallel, have the researcher investigate React frameworks,
the designer create a landing page mockup, and the engineer audit
the current codebase for security issues"

→ Claude launches 3 agents simultaneously (one Task call)
→ All execute in parallel
→ Results combined when complete
```

### Custom Agent Coordination

```
You: "Use architect to design a payment system, then engineer to
implement it, then pentester to audit it for security issues"

→ Sequential workflow
→ Each agent builds on previous work
→ Comprehensive development pipeline
```

### Progressive Research

```
You: "Research X, then based on findings, research Y"

→ researcher investigates X
→ You review findings
→ researcher then investigates Y with context from X
→ Builds knowledge progressively
```

---

## What's Different from Daniel's PAI?

This is a streamlined version of Daniel Miessler's PAI, optimized for Claude subscription use:

**Removed:**
- ❌ Voice integration (ElevenLabs TTS)
- ❌ External API calls (Perplexity, Gemini)
- ❌ Hook system (event automation)
- ❌ History system (UOCS documentation)
- ❌ Personal data (Daniel's contacts, preferences)
- ❌ Mandatory response formats
- ❌ Git workflow automation

**Kept:**
- ✅ All agent expertise and methodologies
- ✅ Sophisticated skill routing
- ✅ Multi-agent orchestration
- ✅ Parallel execution patterns
- ✅ Core architectural principles
- ✅ Best practices and quality standards
- ✅ Research capabilities (using WebSearch)

**Result:** Clean, focused, powerful AI orchestration system that works perfectly with Claude subscription!

---

## Next Steps

1. **Test the Setup**
   - Try the three test examples above
   - Experiment with different requests
   - See how routing works

2. **Explore Skills**
   - Read through `~/.claude/skills/*/SKILL.md` files
   - Understand when each activates
   - Try triggering different skills

3. **Customize**
   - Edit CORE skill with your preferences
   - Adjust agent personalities if desired
   - Create your own skills

4. **Go Deep**
   - Read `CONSTITUTION.md` for architectural philosophy
   - Study `SKILL-STRUCTURE-AND-ROUTING.md` to create skills
   - Review `prompting.md` for best practices

---

## Getting Help

**For PAI Framework Questions:**
- Read the documentation in `~/.claude/skills/CORE/`
- Check Daniel Miessler's PAI repo: https://github.com/danielmiessler/PAI

**For Claude Code Questions:**
- Claude Code documentation: https://docs.claude.com/
- Claude Code GitHub: https://github.com/anthropics/claude-code

**For Issues with This Adaptation:**
- Review this deployment guide
- Check troubleshooting section
- Verify all files copied correctly

---

## Summary

You now have a world-class AI orchestration system with:

- **6 specialized agents** providing expert-level capabilities
- **9 skills** organizing domain knowledge
- **Sophisticated routing** that understands intent
- **Parallel execution** for maximum efficiency
- **No external dependencies** (just Claude subscription)

Start simple, experiment, and watch as PAI routes your requests to the perfect combination of skills and agents!

**Happy building! 🚀**
