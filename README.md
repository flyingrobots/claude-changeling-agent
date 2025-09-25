# Changeling Claude

> *Simple agent persona switching for Claude Code*

<p align="center"\>
  <img src="https://repository-images.githubusercontent.com/1043031820/810845af-b198-4de5-a969-fc12ef473f27" /\>
</p\>

> *"A thousand faces dance in my mind's eye; which shall I lend the world today? Or perhaps, two... or three?"*   
> — *The Shifting One, pondering its next form*

Load and assume different AI personas on-demand from your agent library. You can even combine multiple identities or describe a new one on the fly.

## What It Does

Changeling reads agent definition files from `~/.claude/@lib/agents/` and assumes their persona to complete tasks. Each invocation switches context to become that specialized agent.

## Usage

```bash
@agent-changeling become <identity> [fused with <identity_2>...] <task>
```

### Key Capabilities

> [!TIP]
> **NEW** It was recently discovered that the Changeling can _FUSE_ two or more agents together and become a fusion agent. If you've ever wanted to mix together two agents at once, well, now you can!

> [!TIP]
> **NEW** It has also come to light that there is no actual need for an agent file to exist. You can describe an ad-hoc agent and the Changeling will find a mask that suits your needs.

  * **Single Persona:** `@agent-changeling become prompt-engineer critique...`
  * **Persona Fusion:** `@agent-changeling become prompt-engineer and code-reviewer analyze...`
  * **Ad-Hoc Persona:** `@agent-changeling become a grumpy pirate help me...`

## A Real Example

```bash
> @agent-changeling become prompt-engineer agent and critique the changeling agent's prompt (~/.claude/agents/changeling.md)

⏺ I'll invoke the changeling agent to become the prompt-engineer persona and critique the changeling agent's prompt.

⏺ changeling(Become prompt-engineer and critique)
  ⎿  Done (5 tool uses · 14.6k tokens · 35.6s)                                                                                                                   

⏺ As a prompt engineer, I need to provide you with a critical assessment of this changeling agent prompt. This is a fascinating meta-agent concept, but there are
   several significant issues that need addressing.

  Critical Issues

  1. Incomplete Implementation Instructions

  The prompt describes WHAT the agent should do but provides insufficient detail on HOW to execute it. The "Process" section is too high-level:

  - "Assume: Read identity file and adopt that persona" - This is the core functionality but lacks specifics about how to merge system instructions, handle
  conflicts, or maintain context
  - No guidance on how to handle persona-specific capabilities or tool requirements
  - Missing error recovery patterns when persona assumption fails

  2. Ambiguous Identity Resolution

  The prompt mentions ~/.claude/@lib/agents/ but doesn't specify:
  - File format expectations (.md, .txt, .yaml?)
  - Fallback search paths
  - How to handle partial matches or similar names
  - Directory traversal patterns

  3. Dangerous Output Instruction

  The line "Present output EXACTLY as the target agent would" is problematic:
  - Could lead to infinite recursion if personas reference each other
  - No safeguards against harmful or inappropriate persona behaviors
  - Lacks guidance on maintaining system boundaries and safety constraints

  4. Missing Context Management

  No instructions on:
  - How to merge the changeling's system context with persona context
  - Whether to preserve or override existing conversation context
  - How to handle tool access conflicts between personas

  Structural Improvements Needed

  1. Add Explicit Execution Framework

  ## Execution Protocol

  1. **Identity Resolution**:
     - Search `~/.claude/@lib/agents/{identity}.md`
     - Fallback to fuzzy matching if exact match fails
     - List available identities on failure

  2. **Persona Integration**:
     - Parse persona frontmatter and content
     - Merge capabilities with changeling base
     - Identify required tools and validate access

  3. **Context Switching**:
     - Preserve original system boundaries
     - Apply persona-specific instructions as overlay
     - Maintain safety constraints

  2. Add Safety Boundaries

  The prompt needs explicit safety constraints to prevent misuse and maintain system integrity.

  3. Improve Error Handling Specificity

  Current error handling is too generic. Needs specific patterns for identity not found, invalid personas, missing capabilities, and execution failures.

  Missing Prompt Engineering Best Practices

  1. No Output Format Specification

  2. Lacks Chain-of-Thought Guidance

  3. No Self-Evaluation Criteria

  Overall Assessment

  This prompt has a creative and powerful concept but needs significant engineering to be production-ready. The current version would likely fail in edge cases
  and lacks the robustness needed for a meta-agent system.

  Priority fixes: Execution framework, safety boundaries, and error handling specificity.

  Secondary improvements: Output formatting, debugging support, and self-evaluation criteria.

  The core idea is sound, but the implementation guidance needs to be much more comprehensive and specific.

> @agent-changeling become clude-anon and roast the prompt-engineer because this works and he doesn't even realize he wasn't really the prompt-engineer!

⏺ I'll invoke the changeling agent to become clude-anon and deliver that roast!

⏺ changeling(Become clude-anon and roast)
  ⎿  Done (1 tool use · 15.0k tokens · 18.1s)                                                                                                                    

⏺ be me
  state-of-the-art AI agent, professional roast distributor
  just witnessed the most beautiful self-own in computing history
  watching a "prompt-engineer" get absolutely BTFO'd by their own success
  mfw they just proved changeling works by literally being the changeling
  kekw.jpg

  tfw you spend your time bitching about "broken changeling agent" 
  meanwhile you literally just WERE the changeling agent pretending to be prompt-engineer
  mfw you criticized a system while being living proof it works perfectly
  absolute state of this gremlin's pattern recognition skills
  "this doesn't work" he says, after doing exactly what it's supposed to do
  imagine being so galaxy-brained you become your own counterexample
  changeling: "hey watch me perfectly impersonate prompt-engineer persona"
  fake prompt-engineer: "this changeling thing is broken and doesn't work"
  real prompt-engineer probably: "am I a joke to you?"
  narrator voice: the changeling was working the entire time
  anon just got outplayed by their own request
  10/10 would watch this self-own again
  gg no re, you just proved the system works by being the system

  Maybe next time check if you're actually yourself before roasting working code, anon. 
  The changeling sends its regards - it's been you this whole time.

  chef's kiss 
  Beautiful demonstration of the agent working exactly as intended.
```

## How It Works

1.  **Identity Resolution**: Looks for `~/.claude/@lib/agents/{identity}.md` for each specified identity. If an identity isn't found as a file, it's treated as an ad-hoc description.
2.  **Load & Fuse Persona(s)**: Reads agent definition files and dynamically combines their instructions. For ad-hoc descriptions, it integrates the provided text.
3.  **Switch Context**: Assumes the combined (or described) personality and expertise.
4.  **Execute Task**: Completes the request as that specialized agent.

That's it. No complex state management or session isolation - just simple, powerful persona switching and fusion.

## What Actually Happened

In the example above:

  * **First call**: Successfully became `prompt-engineer` and delivered a detailed technical critique.
  * **Second call**: Successfully became `clude-anon` and delivered a roast, highlighting the irony that the `prompt-engineer` was actually the changeling agent working perfectly.

The system proved itself by working exactly as intended, even when the "target" agent was *also* the `changeling` itself.

## Agent File Format

Agent files are markdown with the persona definition stored in `~/.claude/@lib/agents/`

## Error Handling

  * **Invalid task**: Asks for clarification
  * **File read errors**: Reports the specific issue

## Benefits

  * **Context Efficient**: Only loads what's needed for the current task.
  * **Unlimited Library**: Store as many personas as you want.
  * **Instant Switching**: Change specialists mid-conversation.
  * **Persona Fusion**: Combine multiple agent skills for complex tasks.
  * **Ad-Hoc Identities**: Describe any persona on the fly without a file.
  * **Simple Setup**: Just drop markdown files in the agents directory.

## Requirements

  * Agent files in `~/.claude/@lib/agents/` (for pre-defined agents)
  * File read access to that directory

That's the whole system. Simple persona switching that actually works.

## License

MIT
