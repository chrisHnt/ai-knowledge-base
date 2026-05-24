# 🧠 Fiche #006 — agentmemory (rohitg00)

**Source :** https://github.com/rohitg00/agentmemory  
**Catégorie :** Agents IA / Mémoire persistante / MCP  
**Langage :** TypeScript · Licence : Apache 2.0 · ⭐ 11.6k · Forks : 978  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Moteur de mémoire persistante sémantique pour agents de code IA, exposé via MCP. Résout le problème fondamental des agents : **ils oublient tout à la fin de la session**.

L'agent capture silencieusement via des hooks chaque outil utilisé, compresse les observations en mémoire structurée, et réinjecte le bon contexte au début de la session suivante. Résultat : l'agent "sait déjà" ce qui a été fait précédemment — sans re-explication.

---

## 🔍 Problème résolu

```
Session 1 : "Ajoute de l'auth à l'API"
  → L'agent code, teste, corrige
  → agentmemory capture chaque tool use silencieusement
  → Fin de session : observations compressées en mémoire structurée

Session 2 : "Ajoute maintenant le rate limiting"
  → L'agent sait déjà :
    - L'auth utilise JWT middleware dans src/middleware/auth.ts
    - Les tests dans test/auth.test.ts couvrent la validation de token
    - jose a été choisi sur jsonwebtoken pour la compatibilité Edge
  → Zéro re-explication. Démarre immédiatement.
```

---

## ⚙️ Fonctionnement

### Pipeline mémoire
```
PostToolUse hook → SHA-256 dédup (fenêtre 5min) → filtre privacy
  → stockage observation brute
  → compression LLM → faits structurés + concepts + narrative
  → embedding vectoriel (6 providers + local)
  → index BM25 + vecteur

Stop/SessionEnd → résumé session → extraction knowledge graph

SessionStart → profil projet (top concepts, fichiers, patterns)
  → recherche hybride (BM25 + vecteur + graphe)
  → budget tokens (default 2000) → injection contexte
```

### 4 tiers de mémoire (analogie mémoire humaine)
| Tier | Quoi | Analogie |
|---|---|---|
| Working | Observations brutes des tools | Court terme |
| Episodic | Résumés de sessions compressés | "Ce qui s'est passé" |
| Semantic | Faits et patterns extraits | "Ce que je sais" |
| Procedural | Workflows et patterns de décision | "Comment faire" |

### Recherche triple-stream
| Stream | Méthode |
|---|---|
| BM25 | Keyword matching stemisé + expansion synonymes |
| Vector | Cosine similarity sur embeddings denses |
| Graph | Traversée knowledge graph via entity matching |
Fusion via Reciprocal Rank Fusion (RRF, k=60).

---

## 📊 Benchmarks (LongMemEval-S, ICLR 2025)

| Système | R@5 | R@10 | MRR |
|---|---|---|---|
| **agentmemory** | **95.2%** | **98.6%** | **88.2%** |
| BM25-only fallback | 86.2% | 94.6% | 71.5% |

**Tokens/an** : ~170K (vs 19.5M+ en paste full context) → **92% d'économie**.

---

## 🚀 Installation

```bash
# Démarrer le serveur
npm install -g @agentmemory/agentmemory
agentmemory  # port 3111

# Claude Code — plugin complet (hooks + MCP + skills)
/plugin marketplace add rohitg00/agentmemory
/plugin install agentmemory

# Vérification
curl http://localhost:3111/agentmemory/health

# Viewer temps réel
open http://localhost:3113
```

### Config MCP universelle (Cursor, Cline, Windsurf, Gemini CLI…)
```json
{
  "mcpServers": {
    "agentmemory": {
      "command": "npx",
      "args": ["-y", "@agentmemory/mcp"],
      "env": { "AGENTMEMORY_URL": "http://localhost:3111" }
    }
  }
}
```

---

## 🛠️ 51 outils MCP exposés

Catégories principales : recall, save, smart search, sessions, timeline, profile, patterns, graph query, consolidate, team share, audit, governance delete, snapshots, actions (avec dépendances), leases multi-agents, signals inter-agents, sentinels événementiels, diagnostics, heal.

**Mode standalone (7 outils de base sans serveur) :**
```bash
npx -y @agentmemory/mcp  # mode shim local
```

---

## 🆚 vs mémoire built-in

| | CLAUDE.md built-in | agentmemory |
|---|---|---|
| Scale | 200 lignes max | Illimité |
| Recherche | Tout en contexte | BM25 + vecteur + graph (top-K seulement) |
| Tokens | 22K+ à 240 obs | ~1900 tokens (92% moins) |
| Cross-agent | Fichiers par agent | MCP + REST (tout agent) |
| Coordination | Aucune | Leases, signals, actions, routines |

---

## 🔒 Privacy

- Clés API, secrets, tags `<private>` filtrés avant stockage
- Serveur bind sur `127.0.0.1` par défaut
- Viewer (port 3113) accessible uniquement en local
- Pas de DB externe (SQLite + iii-engine)

---

## 📌 Pertinence pour ce projet

- **Solution #1 au problème de mémoire des agents locaux** : plug-and-play via MCP sur tout agent compatible
- **Économie de tokens critique** pour les modèles locaux avec fenêtre limitée
- **Knowledge graph** : l'agent construit une représentation structurée de ton codebase au fil du temps
- **Multi-agent** : leases + signals pour coordonner plusieurs agents sur un même projet
- **Session replay** : rejouer les sessions Claude Code passées (import JSONL `~/.claude/projects`)

**Tags :** `mémoire-persistante` · `mcp` · `semantic-search` · `vector-db` · `local-ai` · `claude-code` · `multi-agent`
