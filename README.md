# Agent Skills

Reusable Codex skills and plugins maintained by Surajit Das.

## Install the marketplace

Add this repository as a Codex plugin marketplace:

```bash
codex plugin marketplace add surajit003/agent-skills
```

Restart Codex if the marketplace does not appear immediately. Open the Plugins Directory, select **Surajit's Agent Skills**, and install the plugin you want.

## Available plugins

### Readable Python

Guides Codex to design, implement, review, and refactor Python modules using explicit operational flow, descriptive naming, nearby helpers, stateful classes only when needed, and minimal abstraction.

Explicit invocation:

```text
$readable-python Refactor this Python module without changing its behavior.
```

## Repository structure

```text
.agents/plugins/marketplace.json
plugins/
  readable-python/
    plugin.json
    .codex-plugin/plugin.json
    skills/
      readable-python/
        SKILL.md
        agents/openai.yaml
```

## Add another skill

1. Create `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`.
2. Add `.codex-plugin/plugin.json` to the plugin directory.
3. Add the plugin to `.agents/plugins/marketplace.json`.
4. Validate the skill and plugin locally.
5. Commit and push the new version.

Developers who already installed the marketplace can retrieve updates with:

```bash
codex plugin marketplace upgrade surajit003-agent-skills
```

This repository currently has no open-source license. Add an appropriate license before permitting redistribution or modification beyond marketplace installation.
