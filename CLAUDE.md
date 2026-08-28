# Claude Code — Cartelis Cowork Plugins

Tu es dans la **marketplace Claude (Code / Cowork / Web)** des plugins maintenus par Cartelis. Manifest racine : `.claude-plugin/marketplace.json`.

## Besoin métier de ce repo

Embarquer dans Claude tout ce qui ne tient pas dans un `.md` du repo méthode : assets binaires (templates `.pptx`, logos, illustrations), runtime Python (`python-pptx`), templates HTML + CSS. Et distribuer aux consultants comme **plugins Claude** installables, pas en demandant à chacun de cloner un dossier.

Repo distinct de `Cartelis-Data/cartelis_main` (méthode texte) parce que les binaires ne doivent pas polluer le contexte LLM du repo méthode, et chaque plugin a son propre cycle de vie / version / owners.

## Tu n'es ni le lieu d'utilisation ni le repo méthode

Les vrais plugins utilisés au quotidien vivent dans Claude (Code / Cowork / Web), installés par les consultants depuis ce marketplace. Tu touches ici **uniquement aux sources** : manifest, skills internes, assets, scripts. La méthode (skills repo, doctrines, catalogue) est dans `Cartelis-Data/cartelis_main` — qu'on ne touche pas d'ici, sauf via PR séparée sur ce repo méthode si l'usage d'un plugin change.

## Format Claude plugin standard — 2 contraintes critiques

```
plugin-name/
├── .claude-plugin/plugin.json
├── skills/
│   └── skill-name/         racine du skill : SKILL.md + assets + scripts ICI
│       ├── SKILL.md
│       ├── assets/
│       └── scripts/
└── README.md
```

Sans respect strict, l'UI Claude affiche "Ce plugin n'a aucune compétence" :

1. **Skill = dossier + `SKILL.md`** (pas de fichier plat `skills/<name>.md`).
2. **Assets DANS le dossier du skill**, pas à la racine du plugin.

Frontmatter SKILL.md : au moins `description:` (le `name:` vient du dossier). Slash command : `/<plugin-name>:<skill-name>`.

## Workflow modification

1. Brancher, modifier les assets / scripts / SKILL.md du plugin
2. Bumper `<plugin>/.claude-plugin/plugin.json` (semver)
3. **Bumper la même version dans `.claude-plugin/marketplace.json` racine** (sinon les clients déjà abonnés ne voient pas la nouvelle version)
4. PR + review Slack `#cartelis_claude`
5. Merge `main` → tag (ex. `pptx-v1.2`)
6. Annoncer Slack `#cartelis_claude`

## Gouvernance

- Pas de credentials, PII, données client commit dans ce repo
- **Ne jamais ajouter de `Co-Authored-By: Claude …` dans les messages de commit**
- Pas d'emoji dans les fichiers lus par l'IA
- Pas de schéma ASCII complexe dans les skills embarqués (prose ou bullets)

## Install Claude Code (rappel)

```
/plugin marketplace add Cartelis-Data/cartelis_cowork_plugins
/plugin install <plugin-name>@cartelis-cowork-plugins
```

Côté Claude Web / Cowork : install via UI marketplace. Normalement déjà déployé au niveau orga Cartelis.
