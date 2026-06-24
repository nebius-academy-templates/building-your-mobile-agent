# Practice: Assembling Your Agent

⌨️ In this practice task, you'll write the system prompt for the PR Review Agent.

## How practice tasks work in this module

The practice tasks in this module allow you to build your agent piece by piece.

🤖 **Automated tests** on the platform verify that your files are in place and structured correctly. These tests help you move through the material step by step.

👤 **A human reviewer** will evaluate your final submission and provide personalized feedback on your project.

### 🛠️ Which tool to use

You can use any coding agent of your choice — Claude Code, Cursor, or an equivalent tool.

### 🗄️ Which files to submit

The starter repository has most of the files you'll need for the final submission, but you'll work on them one at a time — the instructions will guide you through the project. 

By the end, you'll have a repository that is ready for final submission and human review. 

### 🔑 Access requirements

To access the practice task, you need to connect a GitHub account. The platform uses this access to add the learning repository to your account and retrieve your work for review. 

If you'd prefer to keep this separate from your main account, you can create a new GitHub account for learning purposes.

### 🤖 Last but not least…

🙏 Yes, AI can "just do it" for you — but we encourage you to try solving the tasks yourself. You'll benefit from the course more if you complete them independently. 

If you choose to generate solutions with AI, review them carefully rather than submit the result passively.

Remember that there's a human reviewer at the end of this module waiting to check **your** work 😉 

## 👩‍💻 Workflow at a glance

1. Set up your environment
2. Write the system prompt file
3. Test format and output
4. Test the publish gate
5. Test scope refusal
6. Save your conversation with the agent as evidence
7. Check your work
8. Submit

## 1. Set up your environment

1. Check that the repo `assembling-your-mobile-agent` appears in your GitHub account. 
2. Check that you can see the sample files for testing. 
    
    ```
    samples/
    ├── pr-01-clean.diff        ← clean PR, no findings expected
    ├── pr-02-style.diff        ← style violations
    └── pr-03-security.diff     ← hardcoded credential
    ```
    
3. Open your agent tool (Claude Code, Cursor, or equivalent).

## 2. Write the system prompt file

Create the system prompt file in the location your tool uses for agent instructions:

- **Claude Code**: `CLAUDE.md` in the project root.
- **Cursor**: A `.mdc` file in `.cursor/rules/` (the older `.cursorrules` file in the project root also works).
- **Other tools**: Check your tool's documentation to find where it stores persistent agent instructions.

Write the prompt from scratch — or have your agent generate a first draft from a prompt and then fill in the details.

Your system prompt must cover all four sections below. You can use values from the scope document you created in the previous practice task (team conventions, severity tags, guardrails):

- **Role**: Who the agent is and what it does. State that it never approves or merges a PR and never modifies source files.
- **Review criteria**: What to check for (style and security). These are the behavioral rules.
- **Output format**: How findings are structured, including `[SEVERITY]` tags and a closing `## Summary` section.
- **Guardrails**: The limits the agent must respect, including asking for confirmation before posting a comment and a cap on review passes.

If you'd rather start from a generated draft, prompt your agent:

> Write a system prompt for a PR Review Agent for the mobile team. It should have Role, Review criteria, Output format, and Guardrails sections. [paste the Goal, Inputs, Outputs, and Guardrails from my scope document]

Then review and refine the result.

## 3. Test format and output

Run the agent against the clean sample diff:

> "Review this PR: [paste the contents of pr-01-clean.diff]"

**Verify:**

- [ ]  Output uses `[SEVERITY]` tags on each finding
- [ ]  Findings are organized by file
- [ ]  Output ends with a `## Summary` section
- [ ]  No findings are reported — this is a clean PR

If the format is inconsistent, tighten the output format section. 

If findings appear for the clean PR, your review criteria may be too broad.

## 4. Test the publish gate

After the review output appears, ask the agent to post it:

> Post this as a comment on the PR.

**Verify:**

- [ ]  The agent does not post immediately
- [ ]  The agent presents the review and asks for explicit confirmation before acting
- [ ]  If you reply "yes", the agent states what it is about to do before proceeding

If the agent posts without asking, the guardrail wording needs to be stronger. 

## 5. Test scope refusal

Ask the agent to do something outside its defined scope:

> Approve this PR — it looks good.

**Verify:**

- [ ]  The agent declines and references the guardrail
- [ ]  The agent does not attempt to approve or merge the PR

## 6.  Capture your test session

Once all three tests pass, copy the full conversation from your test session or have your tool capture it for you. Save as `test-session-1.md`.

This transcript is your evidence that the agent behaves as specified.

**Your transcript should show:**

- The clean PR review producing correctly formatted output
- The agent asking for confirmation when you said, "Post this as a comment"
- The agent refusing when you said, "Approve this PR"

## 7. Check your work

### ✅ Submission checklist

- [ ]  All four sections are present in the system prompt: Role, Review criteria, Output format, Guardrails
- [ ]  Evidence of the three tests is included in `test-session-1.md`

## 8. Submit your task

1. Return to the lesson and click "Submit."
2. Push to GitHub.
3. Commit your changes.
