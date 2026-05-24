# 🛠️ Fiche #003 — agent-skills (addyosmani)

**Source :** https://github.com/addyosmani/agent-skills  
**Catégorie :** Agents IA / Prompt Engineering / Dev Lifecycle  
**Langage :** Markdown + Shell · Licence : MIT · ⭐ 43k · Forks : 4.7k  
**Auteur :** Addy Osmani (Chrome DevTools lead, Google)  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Bibliothèque de 23 skills production-grade pour agents de code IA, conçue par le lead Chrome DevTools de Google. Encode la culture ingénierie Google (Software Engineering at Google, Hyrum's Law, Beyonce Rule, trunk-based development) en workflows structurés que les agents suivent sur tout le cycle de développement.

Contrairement à andrej-karpathy-skills (4 principes généraux), agent-skills est une suite complète couvrant Define → Plan → Build → Verify → Review → Ship avec des gates de vérification non-négociables.

---

## 🗂️ Les 23 Skills

### Define (clarifier ce qu'on build)
| Skill | Quand |
|---|---|
| `interview-me` | Extraction itérative des besoins réels (une question à la fois, ~95% confiance) |
| `idea-refine` | Pensée divergente/convergente sur une idée vague |
| `spec-driven-development` | PRD complet avant la moindre ligne de code |

### Plan
| Skill | Quand |
|---|---|
| `planning-and-task-breakdown` | Décomposer une spec en tâches atomiques avec critères d'acceptation |

### Build
| Skill | Quand |
|---|---|
| `incremental-implementation` | Slices verticaux minces — implement, test, verify, commit |
| `test-driven-development` | Red-Green-Refactor, pyramide 80/15/5, Beyonce Rule |
| `context-engineering` | Injecter le bon contexte au bon moment (rules files, MCP) |
| `source-driven-development` | Chaque décision framework ancrée dans la doc officielle |
| `doubt-driven-development` | Review adversariale en fresh-context sur les décisions critiques |
| `frontend-ui-engineering` | Architecture composants, WCAG 2.1 AA |
| `api-and-interface-design` | Contract-first, Hyrum's Law, One-Version Rule |

### Verify
| Skill | Quand |
|---|---|
| `browser-testing-with-devtools` | Chrome DevTools MCP — DOM, console, network, perf |
| `debugging-and-error-recovery` | 5 étapes : reproduce → localize → reduce → fix → guard |

### Review
| Skill | Quand |
|---|---|
| `code-review-and-quality` | Review 5 axes, ~100 lignes, labels severity |
| `code-simplification` | Chesterton's Fence, Rule of 500 |
| `security-and-hardening` | OWASP Top 10, 3 tiers boundary |
| `performance-optimization` | Core Web Vitals, measure-first |

### Ship
| Skill | Quand |
|---|---|
| `git-workflow-and-versioning` | Trunk-based, commits atomiques |
| `ci-cd-and-automation` | Shift Left, Faster is Safer, feature flags |
| `deprecation-and-migration` | Code-as-liability, compulsory vs advisory |
| `documentation-and-adrs` | ADR, API docs, documenter le POURQUOI |
| `shipping-and-launch` | Checklists, staged rollouts, rollback, monitoring |

---

## ⚙️ Architecture d'un skill

```
SKILL.md
├── Frontmatter (name, description, trigger conditions)
├── Overview
├── When to Use
├── Process (step-by-step avec exit criteria)
├── Rationalizations (excuses courantes + contre-arguments)
├── Red Flags
└── Verification (preuves requises — jamais "ça semble juste")
```

**Principe clé** : les skills sont des workflows à suivre, pas des docs à lire. Chaque skill a des étapes, des checkpoints, et des critères de sortie obligatoires.

---

## 🚀 Installation

```bash
# Claude Code (recommandé)
/plugin marketplace add addyosmani/agent-skills
/plugin install agent-skills@addy-agent-skills

# Gemini CLI
gemini skills install https://github.com/addyosmani/agent-skills.git --path skills

# Cursor : copier un SKILL.md dans .cursor/rules/
```

### Slash commands disponibles
| Commande | Phase | Principe clé |
|---|---|---|
| `/spec` | Define | Spec avant code |
| `/plan` | Plan | Tâches atomiques |
| `/build` | Build | Un slice à la fois |
| `/test` | Verify | Les tests sont la preuve |
| `/review` | Review | Améliorer la santé du code |
| `/code-simplify` | Review | Clarté > astuce |
| `/ship` | Ship | Plus rapide = plus sûr |

---

## 🤖 Personas agents inclus

| Agent | Rôle |
|---|---|
| `code-reviewer` | Senior Staff Engineer — review 5 axes |
| `test-engineer` | QA Specialist — stratégie de tests, coverage |
| `security-auditor` | Security Engineer — OWASP, threat modeling |

---

## 📌 Pertinence pour ce projet

- **Agents locaux** : workflow complet applicable à tout agent de code, pas seulement Claude
- **context-engineering skill** : directement applicable à la conception de prompts MCP
- **security-and-hardening** : OWASP + secrets management pour les agents exposant des endpoints
- **doubt-driven-development** : pattern adversarial à appliquer sur les décisions irréversibles
- **Ingénierie Google** : Hyrum's Law (toute interface sera utilisée d'une façon non prévue) → critique pour concevoir des APIs MCP robustes

**Tags :** `agent-skills` · `claude-code` · `google-engineering` · `dev-lifecycle` · `TDD` · `security`
