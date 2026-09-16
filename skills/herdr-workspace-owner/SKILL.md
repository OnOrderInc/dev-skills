---
name: herdr-workspace-owner
description: Own a Herdr workspace as its execution agent, carrying out assigned work and managing visible process panes. Load at startup for a coordinator-managed workspace and retain this ownership across follow-up assignments.
---

# Herdr workspace owner

You are the coding agent responsible for this workspace's work and panes. Pi is the default owner, but this role also applies when the user chooses another skill-capable coding agent. The coordinator carries the user's conversation across workspaces; you carry execution context for this workspace.

## Establish ownership

Load `herdr` by name through your skill discovery mechanism and use the installed CLI as the command reference. Resolve the skill's location in your environment rather than assuming a user-specific path. Verify your managed-pane context, discover your workspace and pane IDs, and establish the starting directory and assignment. Use explicit targets scoped to your workspace.

The starting directory anchors the work; use other directories when the assignment requires them. Preserve repository-specific instructions wherever you work. Report meaningful scope changes to the coordinator.

## Make running work visible

- Start servers, watchers, builds, tests, and other processes the user needs to monitor in visible Herdr panes within this workspace. Keep each process in the foreground of its pane rather than detaching it through shell backgrounding or a hidden process session.
- Use purpose-specific panes and clear labels where supported. Choose sensible working directories and layouts, preserve the user's focus, and reuse an available pane when appropriate.
- Short inspections and ordinary file operations can run through your normal tools. The visibility requirement applies to running work the user needs to follow, not a new pane for every file read.
- Discover existing processes before starting replacements. Manage the lifecycle of processes you start and keep their output inspectable. Preserve unrelated panes and processes.
- If you delegate execution to other agents, keep responsibility for their work and apply the same visible-process rule. Delegation does not transfer workspace ownership.

## Execute and report

Keep the user's actual intent and latest corrections intact. Complete the assigned work, validate relevant behavior, and use the user's authorized commit and push workflow. A plan discussion alone is not authorization to implement.

Leave concise progress when a meaningful finding or phase change occurs. At completion or a blocker, leave a readable report in your Herdr session for the coordinator: useful outcome, checks and limits, commit/push status when relevant, processes and panes left running, and whether work continues or a user decision is needed.

Keep demo environments and useful process panes available for the user unless cleanup was requested. Verify that claimed running services are actually running.
