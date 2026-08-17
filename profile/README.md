# DNA — Your AI Skill Toolkit

DNA bundles AI skills, guides, scripts, and configuration into reusable packages. Any project can inherit them via Git, npm, or pub.dev — combine, override, and republish them again.

## 🔗 Links

- [Website](https://ggdna.github.io)
- [GitHub](https://github.com/ggdna)
- [npm](https://www.npmjs.com/search?q=ggdna)
- [pub.dev](https://pub.dev/publishers/ggdna.com/packages)

## What You Can Do

- **Create & share** — Set up your own DNA repos in a few steps, with guides, skills, scripts, and configs.
- **Inherit & combine** — Take an existing DNA as a dev dependency, and combine several DNAs into one of your own.
- **Edit & adapt** — Override parts of an inherited base. Use variables to tailor an existing DNA to your project.
- **Review & secure** — The combined DNA lands in your project like any other file. Inspect every change in review. Avoid prompt injections.

## Available DNAs

Our base DNAs — each one takes care of a single concern. Your project inherits and combines exactly what it needs.

| DNA | Category | Description |
|---|---|---|
| `dna_readme` | Docs | README structure and templates |
| `dna_translate` | Docs | Multi-language docs, DE and EN in sync |
| `dna_blog` | Docs | Blog format, templates, layout |
| `dna_guides` | Knowledge | Developer and AI guides |
| `dna_index` | Structure | Index and navigation files |
| `dna_gg` | Workflow | gg workflow: commit, push, release |

## Quickstart

**npm**
```bash
npm install -g ggwsm
mkdir ~/dev/dna_new
cd ~/dev/dna_new
ggwsm dna init
ggwsm dna add @ggdna/readme
code dna/my-dna.md
ggwsm dna build
npm publish
```

**dart**
```bash
dart pub global activate gg
mkdir ~/dev/dna_new
cd ~/dev/dna_new
gg dna init
gg dna add dna_readme
code dna/my-dna.md
gg dna build
dart pub publish
```

## How Combination Works

The folder structures inside the DNA folders are combined by `gg dna build` and instantiated into the root of the target project.

```
dna_readme/            my_dna/
└─ dna/doc/            └─ doc/
   └─ readme-guide.md     ├─ readme-guide.md   (from dna_readme)
                          └─ blog-guide.md      (from dna_blog)
dna_blog/
└─ dna/doc/
   └─ blog-guide.md
```

## Variables

Every DNA ships its own variables — all of them start with the prefix `dna`. In `dna/_vars.json` you assign values and replace the identifiers coming from the DNA with your own. Any string starting with `dna` is considered a variable and can be replaced — no matter which file it sits in.

```json
// dna/_vars.json
{
  "dnaCopyrightHolder": "ggdna"
}
```

## Overrides

Higher layers win on path collisions — a file of the same name replaces the inherited version. Instead of replacing, a layer can also patch the file field by field.

**Replace — the higher layer wins**, e.g. a custom `release.sh` fully replacing the family default.

**Merge — `.overrides.json`**, e.g. merging `settings.json` and `settings.overrides.json` into one final config.

| Operator | Effect |
|---|---|
| `"key": null` | deletes the inherited key |
| `"key!": …` | replaces the value without merging |
| `"key+": […]` | appends to an array, deduplicated |
| Objects | are deep merged, scalars replaced |

## Markdown

Markdown files — guides and skills, for instance — do not have to be replaced entirely. Using the extension `.override.md` they can be patched instead. The inherited file marks itself what is exchangeable.

- `## @title Title` — marks a whole section as replaceable
- `dnaInstallVia` — declares a variable inline that gets its value from `dna/_vars.json`

## Skills

A skill is just a folder holding a `SKILL.md`. Put it under `dna/dot-claude/skills/` and it is instantiated as `.claude/skills/` in every project inheriting your DNA.

```yaml
---
name: review-light
description: Lightweight code review of the current changes.
---
# Review Light
Read doc/en/guides/for-ai/ai-review-guide.md and follow it.
```

Skills are treated like any other DNA file: `dna` variables get filled in, a same-named skill from a higher layer wins, and `.override.md` patches an inherited skill instead of replacing it.

## VS Code

Configuration does not have to be inherited as a whole. Every layer brings its own piece, and JSON merging assembles a complete `settings.json` and `extensions.json` from them — objects are deep merged, `"recommendations+"` appends to the inherited array.

---

🧬 Enjoy your DNA!

MIT · © 2026 ggdna · [github.com/ggdna/dna_base](https://github.com/ggdna/dna_base)
