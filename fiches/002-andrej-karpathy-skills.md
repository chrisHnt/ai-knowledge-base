# 🧠 Fiche #002 — andrej-karpathy-skills (forrestchang)

**Source :** https://github.com/forrestchang/andrej-karpathy-skills  
**Catégorie :** Prompt Engineering / Agent Behavior / Claude Code  
**Langage :** Markdown · Licence : MIT · ⭐ 91k · Forks : 8.7k  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Un fichier `CLAUDE.md` unique dérivé du thread X d'Andrej Karpathy sur les 3 défauts récurrents des agents de code LLM. Intégré dans un projet, il recadre le comportement de Claude Code (ou tout agent similaire) dès le prochain prompt.

Origine : Karpathy liste publiquement ce qui le frustre dans les LLMs de code → un développeur transforme le thread en fichier de guidelines → 91k stars en quelques semaines.

---

## ⚙️ Problèmes adressés

| Problème | Manifestation |
|---|---|
| Hypothèses silencieuses | Le modèle choisit une interprétation sans la signaler ni demander |
| Surcomplication | Code de 1000 lignes quand 100 suffiraient, abstractions inutiles |
| Effets de bord | Modification de code non lié à la tâche (comments, formatting, dead code) |

---

## 📐 Les 4 principes

**1. Think Before Coding**  
Ne pas supposer. Signaler les ambiguïtés. Présenter les tradeoffs *avant* de coder. Si incertain → demander, pas deviner.

**2. Simplicity First**  
Minimum de code qui résout le problème. Zéro abstraction spéculative, zéro feature non demandée, zéro gestion d'erreur pour des cas impossibles. Règle : si un senior dirait "trop compliqué" → simplifier.

**3. Surgical Changes**  
Toucher uniquement ce qui est nécessaire. Ne pas "améliorer" le code adjacent. Signaler le code mort sans le supprimer. Chaque ligne modifiée doit tracer directement vers la demande.

**4. Goal-Driven Execution**  
Transformer les tâches impératives en critères de succès vérifiables.

| Au lieu de... | Transformer en... |
|---|---|
| "Ajoute une validation" | "Écris des tests pour les inputs invalides, puis fais-les passer" |
| "Corrige le bug" | "Écris un test qui reproduit le bug, puis fais-le passer" |
| "Refactorise X" | "Vérifie que les tests passent avant et après" |

---

## 🚀 Installation

```bash
# Option A : plugin Claude Code (global, recommandé)
/plugin marketplace add forrestchang/andrej-karpathy-skills
/plugin install andrej-karpathy-skills@karpathy-skills

# Option B : par projet (nouveau)
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md

# Option B : par projet (append sur CLAUDE.md existant)
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md >> CLAUDE.md
```

**Cursor :** fichier `.cursor/rules/karpathy-guidelines.mdc` inclus → fonctionne out-of-the-box.

---

## 📦 Fichiers clés du repo

| Fichier | Rôle |
|---|---|
| `CLAUDE.md` | Fichier principal à intégrer dans ses projets |
| `CURSOR.md` | Variante pour Cursor |
| `EXAMPLES.md` | Exemples concrets d'application des 4 principes |
| `.claude-plugin/` | Structure du plugin Claude Code |
| `.cursor/rules/` | Règles Cursor prêtes à l'emploi |

---

## 💡 Insight clé (Karpathy)

> "Les LLMs sont exceptionnellement bons pour boucler jusqu'à atteindre des objectifs spécifiques. Ne leur dis pas quoi faire — donne-leur des critères de succès et laisse-les aller."

Le principe Goal-Driven capture ça : transformer des instructions impératives en objectifs déclaratifs avec boucles de vérification.

---

## 📌 Pertinence pour ce projet

- **Claude Code** : intégration directe via plugin ou `CLAUDE.md` projet
- **Agents locaux** : les 4 principes s'appliquent à tout agent de code, pas seulement Claude
- **Orchestration** : le principe Goal-Driven est directement applicable à la conception de prompts système pour des agents autonomes (définir des critères de succès plutôt que des étapes)
- **Prompt engineering** : référence de base à combiner avec les guidelines projet-spécifiques

**Tags :** `prompt-engineering` · `agent-behavior` · `claude-code` · `best-practices` · `CLAUDE.md`
