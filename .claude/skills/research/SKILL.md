---
name: research
description: Multi-source comprehensive research using intelligent query decomposition and parallel WebSearch execution. USE WHEN user says 'do research', 'research X', 'find information about', 'investigate', 'analyze trends', 'current events', or any research-related request.
---

# Research Skill

## When to Use This Skill

This skill activates when the user requests research or information gathering:
- "Do research on X"
- "Research this topic"
- "Find information about X"
- "Investigate this subject"
- "Analyze trends in X"
- "Current events research"
- Any comprehensive information gathering request

## How Research Works

The research workflow uses two specialized agents working together:

### 1. Researcher (Orchestrator)
The main research coordinator that:
- Determines if research is simple (single perspective) or complex (multi-perspective)
- For simple queries: Uses WebSearch directly
- For complex queries: Spawns multiple claude-researcher agents in parallel

### 2. Claude-Researcher (Specialist)
Specialized research agents that:
- Use Claude's built-in WebSearch tool
- Decompose queries into 3-7 sub-questions
- Execute parallel web searches
- Synthesize findings with source attribution

## Research Workflow

When you receive a research request:

### For Simple Research
```
User Request
    ↓
Launch researcher agent
    ↓
Researcher uses WebSearch directly
    ↓
Returns synthesized findings
```

### For Complex Research
```
User Request
    ↓
Launch researcher agent
    ↓
Researcher decomposes into 3-7 perspectives
    ↓
Researcher spawns 3-7 claude-researcher agents (parallel)
    ↓
Each claude-researcher uses WebSearch for their perspective
    ↓
Researcher synthesizes all findings
    ↓
Returns comprehensive report
```

## Execution Pattern

**For any research request, use the Task tool to launch the researcher agent:**

```
Use Task tool with:
- subagent_type: "researcher"
- prompt: "Research [user's question]"
```

The researcher agent will automatically:
1. Assess complexity
2. Choose single-agent or multi-agent approach
3. Execute research
4. Synthesize findings
5. Return comprehensive results

## Research Capabilities

**Simple Research (Direct WebSearch):**
- Factual lookups
- Current events
- Definition queries
- Single-topic investigations

**Complex Research (Multi-Agent Orchestration):**
- Comparative analysis ("best X for Y")
- Multi-faceted topics
- Trend analysis
- Controversial/nuanced topics
- Deep investigations requiring diverse perspectives

## Speed Benefits

- **Single-agent research**: 15-30 seconds
- **Multi-agent research**: 30-60 seconds (3-7 agents in parallel)
- **Result quality**: Multi-perspective synthesis with source attribution

## Output Quality

All research includes:
- **Comprehensive findings** organized by theme
- **Source attribution** with authority assessment
- **Confidence levels** for major findings
- **Synthesis** of patterns, contradictions, consensus
- **Actionable recommendations** based on research

## Example Usage

**User:** "Research the best React state management library for a large-scale application"

**Your Action:**
1. Launch researcher agent via Task tool
2. Researcher decomposes into perspectives:
   - Performance benchmarks
   - Developer experience
   - Bundle size comparison
   - Ecosystem maturity
   - Production case studies
3. Researcher spawns 5 claude-researcher agents in parallel
4. Each agent researches their perspective
5. Researcher synthesizes findings
6. Returns comprehensive recommendation

**Result:** Multi-perspective analysis in under 60 seconds with high-quality, synthesized insights.
