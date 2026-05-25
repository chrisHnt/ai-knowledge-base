---
titre: NVIDIA Agent Skills
source: https://github.com/NVIDIA/skills
catégorie: Agents IA
langage: Python (skills en Markdown/YAML)
licence: Apache 2.0 + CC BY 4.0
date: 2026-05-25
---

# NVIDIA Agent Skills

## Ce que c'est

Catalogue officiel de **skills (compétences) portables pour agents IA**, publiées et vérifiées par NVIDIA. Une "skill" est un répertoire d'instructions structurées (fichier `SKILL.md` + métadonnées YAML) qui enseigne à un agent IA comment réaliser une tâche spécialisée — sans ré-entraînement, par simple injection de contexte.

Le repo est un **catalog** : il référence les skills maintenues dans les repos produits NVIDIA respectifs, toutes conformes à la spécification ouverte [Agent Skills](https://agentskills.io/specification).

## Fonctionnement

- Chaque skill est un dossier autonome avec un `SKILL.md` à sa racine
- Les métadonnées utilisent du frontmatter YAML (`name`, `description` obligatoires)
- Modèle de **progressive disclosure** : métadonnées légères chargées au démarrage, instructions complètes chargées à l'activation
- Compatible avec tout agent ou framework supportant la spec Agent Skills

### Skills disponibles (mai 2026)

| Produit | Nb skills | Usage |
|---|---|---|
| **cuOpt** | 19 | Optimisation GPU (routing, LP, QP…) |
| **TensorRT-LLM** | 3 | Inférence LLM optimisée |
| **Nemotron Voice Agent** | 1 | Agents vocaux temps réel (Jetson, Cloud NIMs) |
| **NeMo Gym** | 1 | Environnements RL |

### Installation (exemple Claude Code)

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/NVIDIA/cuopt.git
cd cuopt && git sparse-checkout set skills/cuopt-lp-milp-api-python
cp -r skills/cuopt-lp-milp-api-python ~/.claude/skills/
```

Compatible : Claude Code (`~/.claude/skills/`), Codex (`.codex/skills/`), Cursor (`.cursor/skills/`).

## Points notables pour les agents IA locaux

- **Portable** : skills copiables dans n'importe quel agent compatible, pas de dépendance à un framework spécifique
- **Standard ouvert** : suit la spec [agentskills.io](https://agentskills.io/specification), interopérable
- **Activation automatique** : l'agent détecte la tâche pertinente et charge la skill au bon moment
- **Validable** : outil de référence `skills-ref` pour valider ses propres skills
- Les skills TensorRT-LLM sont directement utiles pour l'**inférence LLM locale optimisée**
- Nemotron Voice Agent couvre le **déploiement sur Jetson** (edge/local)

## Usage rapide

1. Identifier la skill utile dans le tableau Available Skills
2. Cloner sparse le repo source (pas le catalog entier)
3. Copier le dossier dans le répertoire `skills/` de ton agent
4. La skill s'active automatiquement sur tâche pertinente

## Pertinence pour ce projet

Très pertinent : propose un **format standard de skills pour agents**, directement réutilisable pour structurer ses propres compétences d'agent local. Le modèle `SKILL.md` + YAML est une bonne pratique à adopter pour documenter les capacités de ses agents. Les skills TensorRT-LLM et Nemotron sont directement exploitables dans un contexte d'IA locale.
