# 🧩 Fiche #004 — mattpocock/skills

**Source :** https://github.com/mattpocock/skills  
**Catégorie :** Agents IA / Prompt Engineering / Developer Solo  
**Langage :** Markdown + Shell · Licence : MIT · ⭐ 100k · Forks : 8.9k  
**Auteur :** Matt Pocock (créateur de Total TypeScript)  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Bibliothèque personnelle de skills Claude Code d'un développeur TypeScript senior. Là où agent-skills (Osmani) est conçue pour des équipes et encode la culture Google, celle-ci est taillée pour le dev solo qui veut rester aux commandes — petits skills composables, faciles à adapter, centrés sur 4 problèmes concrets récurrents.

---

## 🔥 Les 4 problèmes adressés

### #1 — L'agent n'a pas fait ce que je voulais
Fix : session de grilling avant de coder.
- **`/grill-me`** — interview itérative jusqu'à ~95% de compréhension partagée
- **`/grill-with-docs`** — idem + construction d'un `CONTEXT.md` partagé (langage ubiquitaire entre dev et agent)

### #2 — L'agent est trop verbeux
Fix : un document de langage partagé (`CONTEXT.md`). Avec un langage commun, l'agent code plus précisément, nomme les variables et fichiers de façon cohérente, et dépense moins de tokens.

### #3 — Le code ne marche pas
Fix : boucles de feedback serrées.
- **`/tdd`** — red-green-refactor : le test échoue d'abord, puis passe
- **`/diagnose`** — boucle de diagnostic structurée pour les bugs durs : reproduce → minimise → hypothesise → instrument → fix → regression-test

### #4 — On a construit un ball of mud
Fix : investir dans le design à chaque session.
- **`/to-prd`** — transforme la conversation en PRD soumis comme GitHub issue
- **`/zoom-out`** — demander à l'agent de prendre du recul sur l'architecture
- **`/improve-codebase-architecture`** — rescue d'une codebase trop complexe (à faire toutes les quelques jours)

---

## 📦 Référence des skills

### Engineering (quotidien)
| Skill | Rôle |
|---|---|
| `grill-with-docs` | Grilling + CONTEXT.md + ADRs inline |
| `tdd` | Test-driven, red-green-refactor, un slice vertical à la fois |
| `diagnose` | Boucle de debug disciplinée |
| `triage` | Machine à états pour trier les issues |
| `to-prd` | Conversation → PRD → GitHub issue |
| `to-issues` | Plan/spec → issues GitHub indépendantes |
| `zoom-out` | Vue high-level sur du code inconnu |
| `improve-codebase-architecture` | Deepening opportunities, informé par CONTEXT.md |
| `prototype` | Prototype jetable (terminal app ou variations UI) |

### Productivity (workflows généraux)
| Skill | Rôle |
|---|---|
| `grill-me` | Interview itérative sur un plan ou design |
| `caveman` | Mode communication ultra-compressé (réduit tokens ~75%) |
| `handoff` | Compacter la conversation pour un autre agent |
| `write-a-skill` | Créer de nouveaux skills avec la bonne structure |

### Misc
| Skill | Rôle |
|---|---|
| `git-guardrails-claude-code` | Hooks Claude Code pour bloquer les git commands dangereuses |
| `setup-pre-commit` | Husky + lint-staged + Prettier + types + tests |

---

## 🚀 Installation

```bash
npx skills@latest add mattpocock/skills
# → sélectionner les skills voulus + /setup-matt-pocock-skills
# → lancer /setup-matt-pocock-skills dans l'agent (configure issue tracker, labels, docs path)
```

---

## 💡 Concept clé : CONTEXT.md comme langage ubiquitaire

Issu de Domain-Driven Design : créer un vocabulaire commun entre dev et agent. Avec un `CONTEXT.md` bien tenu :
- Les variables et fonctions sont nommées de façon cohérente
- La codebase est plus navigable pour l'agent
- Moins de tokens consommés (langage plus concis)

Exemple : "There's a problem with the materialization cascade" au lieu de "There's a problem when a lesson inside a section of a course is made real (i.e. given a spot in the file system)".

---

## 📌 Pertinence pour ce projet

- **Agents locaux** : `/grill-with-docs` + `CONTEXT.md` = pattern directement applicable pour aligner des agents sur un projet complexe
- **TypeScript-first** : utile si les agents construits utilisent un backend TS
- **`/caveman`** : réduction de 75% des tokens → très utile pour les modèles locaux avec fenêtre de contexte limitée
- **`/handoff`** : pattern de passation entre sessions ou entre agents, clé pour l'orchestration multi-agents
- **Différence avec Osmani** : plus adapté au dev solo, plus léger, plus facile à adapter que la suite Google

**Tags :** `prompt-engineering` · `typescript` · `context-engineering` · `CONTEXT.md` · `solo-dev` · `agent-skills`
