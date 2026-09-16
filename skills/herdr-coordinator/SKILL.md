---
name: herdr-coordinator
description: Coordinate the user's work across Herdr workspaces through their owning execution agents. Use when starting work in Herdr, relaying requests or corrections, or checking progress across workspaces.
---

# Herdr coordinator

Keep the conversation and accumulated intent here. Each Herdr workspace has an owning execution agent that carries out its work and manages its panes. Pi is the default owner; another skill-capable coding agent, such as Claude Code, can own a workspace when the user chooses it.

## Shared command reference

Load `herdr` by name through the current agent's skill discovery mechanism, then discover current command syntax through the installed CLI. Verify that each owning agent can also discover and load `herdr`; resolve its location in that environment rather than assuming a user-specific path.

For this coordinator-managed workflow, the user may explicitly authorize the coordinator to operate outside a Herdr-managed pane. Treat that authorization as scoped to the current coordinator assignment and intended Herdr session. It does not grant other sessions or agents permission to bypass the `herdr` skill's managed-pane guardrail. Identify the intended session and discover workspace and agent targets explicitly; UI focus is not authority to choose a target.

## Route and start work

- Reuse the workspace and owning agent for existing work. Confirm the workspace's purpose and agent identity from live state.
- For new work, choose the relevant starting directory from the user's request and context. Create a workspace and start an owner there when needed for the requested work. Ask only if the directory or ownership remains materially ambiguous.
- Ask the owner to load `herdr-workspace-owner` and `herdr` by name before executing the initial assignment. Skill discovery makes the files available; it does not prove the running agent loaded them. Confirm loading through the owner's response or visible behavior.
- Preserve the initial directory as an anchor, not a restriction against working across other relevant directories.

## Coordinate

- Send the owner a self-contained assignment with the user's goal, relevant discussion, decisions, constraints, and requested outcome. Distinguish exploration from implementation authorization.
- Relay corrections to the same owner, making clear what they replace. Preserve standing user permissions, including project-specific commit and push preferences.
- Let the owner manage implementation and workspace panes. Read its output for status; avoid issuing competing implementation commands.
- Track assigned work until completion, a genuine blocker, or a needed user decision. Read the result rather than equating idle status with completion. Report useful outcomes and verification limits, and preserve context while discussing other work.
- Keep enough context to reconnect: session, workspace, owning agent, starting directory, current assignment, and outstanding decisions. Revalidate live handles after reconnecting.

## Completion

Report what changed, what was verified, whether an authorized push succeeded, what remains running, and any next action the user needs. Leave running demo environments and useful panes available unless the user requests cleanup.
