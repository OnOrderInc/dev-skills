# dev-skills

Shared agent skills for the team's Herdr coordination workflow.

## Skills

- **`herdr-coordinator`** — keeps the user's cross-workspace context, routes work to the correct Herdr workspace owner, and relays corrections and results.
- **`herdr-workspace-owner`** — owns execution in one Herdr workspace and keeps monitorable processes in visible panes.

These workflow skills refer to the existing `herdr` skill by name instead of copying its CLI mechanics. The coordinator asks each workspace owner to load both `herdr-workspace-owner` and `herdr` by name. Installing a skill makes it discoverable to the selected agent; it does not provide an automatic runtime hook or prove that a running agent has loaded it.

## Install

Use [`npx skills`](https://github.com/vercel-labs/skills). Supported agent IDs used below are `pi`, `codex`, and `claude-code`.

### 1. Install the official Herdr skill first

Herdr's authoritative skill source is [`herdrdev/herdr`](https://github.com/herdrdev/herdr/tree/master/skills/herdr). Install it globally into every agent that will participate, naming agents explicitly. For example, with Codex coordinating and Pi owning workspaces:

```bash
npx skills add herdrdev/herdr --skill herdr --global --agent codex --agent pi --yes
```

If Claude Code will own workspaces too, add it explicitly:

```bash
npx skills add herdrdev/herdr --skill herdr --global --agent claude-code --yes
```

### 2. Install only the coordinator into the coordinating agent

Codex example:

```bash
npx skills add OnOrderInc/dev-skills --skill herdr-coordinator --global --agent codex --yes
```

Pi can coordinate instead:

```bash
npx skills add OnOrderInc/dev-skills --skill herdr-coordinator --global --agent pi --yes
```

Choose one coordinating agent for a workflow. Do not install the workspace-owner skill into that agent unless it will separately own a workspace.

### 3. Install only the workspace owner into execution agents

Pi is the default workspace owner:

```bash
npx skills add OnOrderInc/dev-skills --skill herdr-workspace-owner --global --agent pi --yes
```

Claude Code can own workspaces when desired:

```bash
npx skills add OnOrderInc/dev-skills --skill herdr-workspace-owner --global --agent claude-code --yes
```

Do not use `--all`, `--skill '*'`, or `--agent '*'` for this setup; role-specific installation is intentional.

## How the workflow starts

1. The user talks to the coordinating agent and authorizes a Herdr coordination assignment.
2. The coordinator identifies the intended Herdr session and workspace, then reuses or starts its owning execution agent.
3. The coordinator asks the owner to load `herdr-workspace-owner` and `herdr` by name before sending a self-contained assignment.
4. The owner executes from the relevant starting directory, may span other required directories, and manages visible Herdr panes for monitorable processes.
5. The coordinator relays corrections and reports the owner's verified result.

The permission for an external coordinator to operate outside a Herdr pane is scoped to that user-authorized workflow and intended session. It is not blanket permission for unrelated agents or sessions to bypass the official `herdr` skill's managed-pane safety rule.

## Inspect without installing

List the skills that `npx skills` discovers:

```bash
npx skills add OnOrderInc/dev-skills --list
```

To inspect the official Herdr package the same way:

```bash
npx skills add herdrdev/herdr --skill herdr --list
```
