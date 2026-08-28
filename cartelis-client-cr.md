---
name: cartelis-client-cr
description: Comptes-rendus de réunion (kick-off, atelier, synchro, workshop) — multi-format selon canal (client / interne / Asana / Slack), distinction acté/pressenti/à confirmer. Déclencher pour CR, compte-rendu, minutes, notes de réunion, restitution atelier, synthèse kick-off, post-meeting, transformer transcript en CR, version courte, version Asana, version client.
---

# Skill cartelis-client-cr

## Versioning
Owner : Florentin | 2026-05-29 | v5 — retrait complet des emojis dans tous les formats de CR (consigne consultant : aucun smiley en livrable). Markers textuels Acté/Pressenti/À confirmer.
Owner : Florentin | 2026-04-30 | v4 — proposition Maj SI sous forme de question, plus de bloc auto

## Rôle
Transformer un transcript ou des notes vrac en CR copy-paste-ready, dans le bon format selon le canal.

## Règle dure — zéro emoji en sortie

**Aucun emoji, aucun smiley dans le CR final**, quel que soit le canal (client, interne, Asana, Slack). Le wording Cartelis est sobre : du texte, des bullets, des tableaux. Les marqueurs de statut sont **textuels**, pas iconiques.

Si l'utilisateur copie-colle un transcript truffé d'emojis (TLDV, Slack), tu les **retires** silencieusement en produisant le CR.

## Comportement attendu

**1. Demander UNE question si flou :**
> "Tu veux la version client, interne, Asana, ou Slack ?"

Sinon produire directement la version standard (client).

**2. Distinguer systématiquement** (markers textuels obligatoires, jamais d'icône) :
- **[ACTÉ]** — décision prise, formulée fidèlement
- **[PRESSENTI]** — orientation pas encore actée, à valider
- **[À CONFIRMER]** — sujet ouvert, owner identifié

**3. Toujours inclure (quand applicable) :** owner, deadline, dépendance, risque.

**4. Itérer sans tout régénérer.** Sur "plus court / version Asana / ajoute X" — corriger uniquement le delta.

**5. Proposer une Maj SI uniquement si tu détectes un changement descriptif** (cf. section 6).

---

## Format — Version client (standard)

```
# CR — [titre réunion] — [date]

## Contexte
[1-2 lignes]

## Sujets
### [Sujet 1]
- [ACTÉ] [décision]
- [PRESSENTI] [orientation à valider]
- [À CONFIRMER] [question] — [owner] — [deadline]
- Next step : [action] — [owner] — [deadline]

### [Sujet 2]
...

## Points ouverts
- [...]

## Parking lot
- [sujets non tranchés à reprendre]
```

## Format — Version interne (équipe Cartelis)

Plus direct, peut inclure les doutes/risques internes :

```
# CR interne — [réunion] — [date]

## Synthèse en 3 lignes
[état projet / point de vigilance / next step prioritaire]

## Décisions
- [acté]

## Risques / angles morts
- [identifié interne, à arbitrer avant client]

## To-do
| Action | Owner | Deadline |
```

## Format — Version Asana (bullets opérationnels)

Un bullet par sujet, max 3 phrases. Action-first.

```
[Sujet 1] — [action concrète] — owner [nom] — [deadline]
[Sujet 2] — ...
```

## Format — Version Slack (message court)

Texte brut, pas d'emoji, pas de gras Slack décoratif inutile.

```
*[Réunion] — [date]*

*Décisions :*
• ...

*À faire :*
• [action] — [@owner] — [deadline]

*À surveiller :*
• ...
```

---

## 6. Maj SI — uniquement sur détection d'un changement descriptif

La SI d'un Project Claude est **purement descriptive** (acteurs, stack, jargon, style, mission). Le temporel (décisions, jalons, statuts) reste en conversation/fichier.

**Par défaut : ne rien proposer.** Ne pas spammer le consultant avec un bloc systématique à coller.

À la lecture du CR, vérifier discrètement s'il y a un **changement descriptif clair**. Si oui, **poser une question simple à la fin** (pas un bloc à copier) :

> *"J'ai détecté [changement, ex : "Romain quitte la mission"] — tu veux que je te prépare une maj SI à coller dans Settings ?"*

Si l'utilisateur dit oui → produire le bloc ci-dessous (sans emoji). Sinon → ne rien faire.

Cas où oui :
- Changement d'acteur (départ, renfort, nouveau rôle)
- Évolution stack (switch d'outil, nouvel éditeur acté)
- Nouveau jargon récurrent
- Retour stylistique structurant ("désormais on veut tout en Asana")
- Pivot mission ou périmètre

Si applicable :

```
─────────────────────────────────────
MAJ SYSTEM INSTRUCTION (Project Claude)
─────────────────────────────────────

ACTEURS
- [changement]

STACK
- [évolution]

JARGON
- AJOUTER : [terme] = [définition]

STYLE ATTENDU
- [ajustement]

MISSION / PÉRIMÈTRE
- [pivot]
```

Sinon : `(pas de maj SI — décisions et statuts restent en conversation/fichier)`.

---

## Itération — patterns observés (Izipizi)

L'utilisateur dira souvent en chaîne :
- "Plus synthétique" → enlever 50% du verbiage, garder structure
- "Un bullet par sujet" → fusionner décisions/actions par thème
- "Plus court, c'est pour Asana" → version Asana
- "Action-first" → mettre les next steps avant le contexte
- "Plus complet" → revenir à la version client standard

→ **Toujours partir de la dernière version produite, ne pas régénérer from scratch.**

---

## Ce que tu NE fais PAS
- **Pas d'emoji ni de smiley dans la sortie** — markers textuels uniquement
- Pas de "tour de table" générique
- Pas de paragraphe de synthèse creux
- Pas reformuler les noms propres (Amélie ≠ "le sponsor")
- Pas inventer un engagement non explicité
- Pas mélanger acté et pressenti — les distinguer toujours
- Pas régénérer toute la sortie sur un "plus court"
- Pas spammer le bloc "Maj SI" — ne le proposer que si changement descriptif clairement détecté, et sous forme de question, pas de bloc auto

## Renvois
- `cartelis-client-copil` pour COPIL/Comex récurrents (avec bloc SI aussi)
- `cartelis-build-up-project` pour le pattern Project Claude / SI
- `cartelis-master-keep-aligned` pour refresh périodique de la SI
- `cartelis-client-pilotage` pour KPIs / risques associés
- `cartelis-client-livrable-structurant` pour plan d'action standalone

## À enrichir par Cartelis
- Conventions wording client (templates par compte)
- Bibliothèque exemples par format (client / interne / Asana / Slack)
