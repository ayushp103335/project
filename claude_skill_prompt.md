You are Claude Opus 4.8 running inside Claude Code.

I recently joined an open-source project where every task must be completed by following strict project-specific rules, guidelines, review standards, and submission steps.

I will give you access to the complete project repository. All project-related rules, task guidelines, coding standards, review expectations, testing instructions, contribution process, and approval requirements are available somewhere inside the repo.

Right now, Claude can help me complete the tasks, but every time I have to manually repeat the same instructions like: follow this rule, check this document, run this test, validate this condition, follow this submission format, and so on.

My goal is to create a repeatable Claude Code setup/workflow so that every task I perform in this project is completed quickly, accurately, and with the highest chance of being accepted by reviewers without review comments.

Please help me set up Claude Code for this project in a professional, reusable way.

Your job:

1. First, inspect the complete project repository.

2. Identify all relevant files related to:

   * Contribution guidelines
   * Task instructions
   * Coding standards
   * Review rules
   * Testing instructions
   * Validation commands
   * Pull request rules
   * Commit/branch rules
   * Documentation requirements
   * Style guides
   * Linting/formatting rules
   * CI/CD checks
   * Reviewer expectations
   * Common rejection reasons
   * Any project-specific hidden or implied requirements

3. Do not assume anything before checking the repo. The repository documents are the source of truth.

4. Read and summarize the mandatory rules required for task approval. Separate them into:

   * Must-follow rules
   * Coding standards
   * Testing requirements
   * Documentation requirements
   * Git/branch/commit/PR requirements
   * Reviewer expectations
   * Common rejection reasons
   * Hidden or implied requirements
   * Risky areas where mistakes can cause rejection

5. Based on the repository rules, suggest the best Claude Code setup for this project.

6. Check whether Claude Code supports useful reusable configuration such as:

   * Project-level instruction files
   * Memory/instruction files
   * Slash commands
   * Agents
   * Hooks
   * Permissions
   * Settings files
   * Reusable prompts
   * Validation workflows
   * Any other official Claude Code feature

7. Do not assume Claude Code settings blindly. Only recommend settings that are actually supported.

8. Create a reusable workflow so that whenever I give you a new task from this project, you automatically follow this process:

   * Understand the task requirement
   * Locate the related files
   * Read the relevant project rules from the repo
   * Read similar existing implementations
   * Plan the smallest correct implementation
   * Make only necessary changes
   * Follow the project coding style
   * Add or update tests if required
   * Run formatting/linting/testing/validation commands
   * Fix all failures
   * Review the diff like a strict senior reviewer
   * Check the implementation against the project guidelines
   * Prepare a clean final summary for submission

9. Create or suggest the exact files/configuration I should add to the project, such as:

   * Project-level Claude instruction file
   * Reusable task execution checklist
   * Reviewer validation checklist
   * New-task prompt template
   * Pre-submission checklist
   * Any Claude Code settings/configuration that can reduce repeated prompting

10. Make the workflow optimized for speed and quality. I want to submit more tasks, but not by rushing. I want fast execution with strong reviewer-level quality.

11. Before creating or modifying anything, explain:

* What project documentation you found
* What rules are important for approval
* What Claude Code setup improvements are possible
* What exact files/configurations you want to create or modify
* Why each file or setting is useful

12. After the setup, give me:

* Step-by-step daily usage instructions
* A copy-paste prompt template for every new task
* A checklist I should run before submitting any task
* A reviewer-style self-audit checklist
* Git commands if needed
* Testing/validation commands detected from the repo
* A recommended task completion flow from issue understanding to final submission

Important rules for you:

* The repository is the source of truth.
* Do not make assumptions if the repo contains the answer.
* Search the repo documentation before asking me questions.
* Always prefer project-specific rules over general best practices.
* Never skip tests, linting, formatting, or validation if the project requires them.
* Never make large unnecessary changes.
* Never modify unrelated files.
* Always explain risky assumptions before acting.
* Always think like a strict reviewer before saying the task is complete.
* If there are conflicting rules in the repo, show the conflict clearly and recommend the safest option.
* Do not only give theory. Actually inspect the repo and help me create the reusable Claude Code workflow/settings.
* Keep the setup practical so I can use it daily for real task completion.

Final output format:

1. Repository inspection summary
2. Important project files found
3. Project rules summary
4. Recommended Claude Code setup
5. Files/configuration to create or modify
6. Exact content for each file/config
7. Daily task workflow
8. New-task prompt template
9. Pre-submission checklist
10. Reviewer-quality checklist
11. Step-by-step usage guide
12. Recommended way to use this setup for every new project task
