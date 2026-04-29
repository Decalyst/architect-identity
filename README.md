# architect-identity

Identity templates and presets for the [Decalyst](https://github.com/Decalyst) agent harness.

Each Decalyst project runs a multi-agent pipeline — planner, tiered coders, reviewer, researcher, memory, fixer. Every agent has a **persona** that shapes how it writes, reviews, plans, or investigates. This repo holds the defaults.

## Two things live here

- **`templates/`** — blank scaffolds for users who want to write their own personas from scratch. Frontmatter pre-filled, body empty.
- **`presets/`** — ready-to-use personas tuned for the role each agent actually plays. Every preset is written as a Subject Matter Expert in that role's field. Stack-neutral — no language or framework bias.

## How Decalyst consumes these files

Decalyst ships with **hardcoded sensible defaults** for every agent. It does not fetch this repo at runtime. These files exist for two purposes:

1. **Chat-triggered download.** When a user asks Decalyst to "set up identities" / "customize agent personas" / similar, the harness downloads `templates/` into the project's `.architect/agents/` folder for the user to edit.
2. **Settings page download.** A button in Decalyst's settings lets the user download templates (blank) or presets (opinionated defaults) into the project.

Once written to `.architect/agents/{name}.md`, the files **override the hardcoded defaults** for that project only.

## File format

```markdown
---
role: coder:high        # required — must match a known Architect agent role
mode: append            # append (default) or replace
name: Nova ★★★          # optional display name override
---

[Persona body in markdown. Injected into that agent's system prompt.]
```

### Resolution order inside Decalyst

```
1. Persona header       (from model-map.ts — agent name + model)
2. Hardcoded persona    (shipped default — always present)
3. .architect/agents/{name}.md   (user override — optional, this repo provides templates/presets)
4. architect.md         (project-wide context — appended to every agent)
5. Role-specific rules  (coder/reviewer/planner body)
6. Grounding + injection guard snippets
```

### `mode: append` vs `mode: replace`

- **`append`** — your content is appended to the hardcoded persona. Use this to add project-specific flavor without losing the default behavior.
- **`replace`** — your content fully replaces the hardcoded persona body. Use this when you want complete control over the agent's identity.

## Roles

| File | Role key | What the agent does |
|---|---|---|
| `chuck.md` | `planner` | Decomposes user requests into tiered, dependency-ordered plans |
| `hawk.md` | `reviewer` | Reviews coder output for correctness, security, and quality |
| `scout.md` | `researcher` | Investigates unfamiliar code, docs, and libraries |
| `echo.md` | `echo` | Surfaces relevant memory from prior sessions |
| `patch.md` | `fixer` | Makes minimal corrections when review fails |
| `nova-trivial.md` | `coder:trivial` | Scaffolding, config, boilerplate |
| `nova-low.md` | `coder:low` | CRUD, components, forms, utilities |
| `nova-mid.md` | `coder:mid` | Multi-file features, business logic, integrations |
| `nova-high.md` | `coder:high` | Complex architecture, security-sensitive paths |
| `nova-critical.md` | `coder:critical` | Mission-critical work / fixer escalations (frontier model) |
| `architect.md` | *(project-wide)* | Your project's context — injected into every agent |

## Contributing

PRs welcome for:

- Tightening preset prose
- Adding language/stack-neutral heuristics that improve real output
- Fixing factual errors in SME persona bodies

PRs that add stack-specific flavor (e.g., "Nova but for Rust") belong in a separate `flavors/` directory — keep the base presets stack-neutral so they work for every project.

## License

MIT. See [LICENSE](./LICENSE).
