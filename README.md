# food-delivery-plugin

An AI-agent plugin for food delivery apps (Glovo, Wolt, Bolt Food, Uber Eats, Deliveroo, Just Eat Takeaway brands, foodora and more). Currently packaged for Claude (Claude desktop / Cowork and Claude Code); the skills are plain Markdown `SKILL.md` files, so other agents that support skills can reuse them.

This repo is a Claude plugin marketplace containing **food-delivery**: compare a restaurant's prices across your European food delivery apps (**Glovo, Wolt, Bolt Food, Uber Eats, Deliveroo, Just Eat Takeaway brands, foodora** and more), then build the cart and order on the app you choose — only after your explicit confirmation.

Works wherever these apps deliver. Glovo, Wolt and Bolt Food are verified; the others use a generic method until a real run verifies them (see `plugins/food-delivery/skills/compare-food-prices/references/vendors/`).

## Install

**Claude desktop (Cowork):** in the plugin settings, add the marketplace `valentinludu/food-delivery-plugin` (or its GitHub URL), then install **food-delivery**. You can also install a `.plugin` file built from `plugins/food-delivery`.

**Claude Code:**

```
/plugin marketplace add valentinludu/food-delivery-plugin
/plugin install food-delivery@valentinludu-plugins
```

Or in one step (Claude Code 2.1.275+):

```
/plugin install food-delivery --marketplace valentinludu/food-delivery-plugin
```

Then follow the plugin's [README](plugins/food-delivery/README.md).

## Other agents (planned)

The workflow lives in `plugins/food-delivery/skills/*/SKILL.md` (Markdown + YAML frontmatter). Packaging for other agents can be added next to the Claude one, e.g. `adapters/<agent>/`, reusing the same skills.

## Repository layout

```
.claude-plugin/marketplace.json          # marketplace catalog
plugins/food-delivery/     # the plugin
  .claude-plugin/plugin.json
  skills/check-food-app-logins/
  skills/compare-food-prices/            # + references: apps, settings, report template
  skills/order-food/                     # + references: scheduled-task prompt
```

## Releasing a new version

1. Edit the skills.
2. Bump `version` in `plugins/food-delivery/.claude-plugin/plugin.json`, in `.claude-plugin/marketplace.json`, and in each `SKILL.md` metadata.
3. Add an entry to `CHANGELOG.md`, commit, push. Users get the update from the marketplace.

## Contributing

Issues and PRs welcome — especially new vendors and verified entry URLs / login labels / cart flows in `plugins/food-delivery/skills/compare-food-prices/references/vendors/`. Never commit cookies, tokens, addresses or payment details.

## License

MIT
