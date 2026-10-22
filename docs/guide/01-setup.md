# Set up pstack

This tutorial installs the plugin, checks skill discovery, and runs one representative skill.

## Install the public marketplace

Install the marketplace directly from the public GitHub repository:

```bash
codex plugin marketplace add Aqua-123/pstack-for-codex
codex plugin add pstack-for-codex@pstack-for-codex-local
codex plugin list --json
```

For development, pass the absolute checkout path to `codex plugin marketplace add`. Start a new Codex task after installation so the task receives the refreshed skill catalog.

`codex plugin list --json` confirms the plugin installation. The prompt below checks prompt-time discovery. The automated release smoke validates installed catalog files without claiming model dispatch.

## Check one skill

Open a repository and ask for a read-only trace:

```text
$how explain how this repository validates plugin metadata.
```

Codex resolves `$how` to the installed `pstack-for-codex` namespace. The response should cite code paths and separate observed behavior from inference.

## Install optional agent profiles

The plugin works without custom profiles. To add them, run:

```text
$setup-pstack install the pstack agents for this project.
```

Choose `project` or `user` scope when asked. Project scope writes `.codex/agents/*.toml`. User scope writes `~/.codex/agents/*.toml`. Setup scans both locations for duplicate agent names and refuses to overwrite unowned files.

You can ask each profile to inherit the parent model. To request an explicit model, provide both the model and `reasoning_effort`. Setup writes that pair only when a supported live model list proves it. If the model list is unavailable, setup records `unverified-inheritance` and omits both fields.

The result includes the written paths, receipt path, hashes, and configuration status. New profiles apply to agents spawned after installation.

## Remove or upgrade owned profiles

Invoke `$setup-pstack` with an explicit action and scope:

```text
$setup-pstack inspect the project profiles and their receipt.
$setup-pstack upgrade the project profiles.
$setup-pstack uninstall the project profiles.
```

Upgrade and uninstall touch only receipted files whose current hashes still match. A changed or relocated file produces `review-required` and remains untouched.

Next: [Route work through `$poteto-mode`](./02-poteto-mode.md).

Choose only effort levels advertised for the selected model. `max` is an effort level, not unlimited compute. A written profile does not prove which model served a later agent. Upstream host defaults do not remove a model that Codex still supports, including Sol.

The plugin does not require custom profiles. With no verified profile, roles inherit the parent model. Invoke `$poteto-help` if you want help selecting a budget or deciding whether profile setup is useful.

After setup, you can accept an optional project verification offer. [Create verification skill](../../skills/create-verification-skill/SKILL.md) teaches an agent to drive the real app. [Create formal verification skill](../../skills/create-formal-verification-skill/SKILL.md) checks a high-risk property within explicit bounds. Either offer can be declined without blocking setup.
