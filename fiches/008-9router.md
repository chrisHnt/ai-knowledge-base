# 🔀 Fiche #008 — 9router (decolua)

**Source :** https://github.com/decolua/9router  
**Catégorie :** Agents IA / Optimisation coûts / Routage LLM  
**Langage :** JavaScript (Next.js) · Licence : MIT · ⭐ 12.9k · Forks : 1.9k  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Proxy local qui s'intercale entre tes outils de code IA (Claude Code, Cursor, Codex, Cline…) et les providers LLM. Deux fonctions principales :
1. **Routage multi-provider avec fallback automatique** — ne jamais être bloqué par un quota
2. **Compression RTK** — réduire les tokens envoyés de 20-40% sans perte de qualité

**Point clé pour l'IA locale** : 9router permet d'étendre les quotas des abonnements payants (Claude Code Pro/Max) en les combinant avec des providers gratuits ou pas chers, et normalise tous les formats (OpenAI ↔ Claude ↔ Gemini ↔ Ollama) en une seule interface.

---

## ⚙️ Architecture

```
Ton outil (Claude Code / Cursor / Cline...)
         ↓ http://localhost:20128/v1
    9Router (proxy intelligent)
    ├─ RTK Token Saver (compresse les tool_results)
    ├─ Format translation (OpenAI ↔ Claude ↔ Gemini ↔ Ollama...)
    ├─ Quota tracking temps réel
    └─ Smart fallback 3 tiers
         ↓
    Tier 1 : Abonnement (Claude Code Pro, Codex, Copilot)
         ↓ quota épuisé
    Tier 2 : Cheap (GLM $0.6/1M, MiniMax $0.2/1M)
         ↓ budget limit
    Tier 3 : Gratuit (Kiro AI, OpenCode Free, Vertex $300 crédits)
```

---

## 💡 Fonctionnalités clés

### RTK Token Saver (-20 à -40% tokens input)
Compresse les sorties d'outils (`git diff`, `grep`, `find`, `ls`, `tree`, logs…) avant envoi au LLM. Auto-détection du type de contenu, compression sans perte, fallback silencieux si la compression échoue.

Filtres disponibles : `git-diff`, `git-status`, `grep`, `find`, `ls`, `tree`, `dedup-log`, `smart-truncate`, `read-numbered`, `search-list`.

### Caveman Mode (-65% tokens output)
Injecte un prompt système qui force le LLM à répondre en mode ultra-compressé, substance technique préservée.

### Providers supportés (40+)
**Gratuits :**
- **Kiro AI** : Claude 4.5 + GLM-5 + MiniMax, illimité, OAuth (AWS/Google/GitHub)
- **OpenCode Free** : pas d'auth, modèles auto-fetchés
- **Vertex AI** : $300 crédits GCP nouveaux comptes

**Abonnements (via OAuth) :**
Claude Code, Codex, GitHub Copilot, Cursor

**API Key (pas chers) :**
GLM ($0.6/1M), MiniMax ($0.2/1M), Kimi ($9/mois flat 10M tokens), OpenRouter, DeepSeek, Groq, Mistral, xAI, Perplexity...

**Ollama (local) :** support natif via format translation.

### Multi-compte
Plusieurs comptes par provider, round-robin automatique ou priorité.

### Cloud sync
Synchroniser la config entre machines (providers, combos, settings).

---

## 🚀 Installation et usage

```bash
# Installation globale
npm install -g 9router
9router
# Dashboard : http://localhost:20128/dashboard

# Docker
docker run -d --name 9router -p 20128:20128 \
  -v "$HOME/.9router:/app/data" decolua/9router:latest
```

### Intégration Claude Code
```json
// ~/.claude/config.json
{
  "anthropic_api_base": "http://localhost:20128/v1",
  "anthropic_api_key": "ton-api-key-9router"
}
```

### Intégration Cursor / Cline / Continue
```
Provider: OpenAI Compatible
Base URL: http://localhost:20128/v1
API Key: [depuis le dashboard]
Model: cc/claude-opus-4-6  (ou un combo custom)
```

### Combos (exemples)
```
# Zero cost
free-forever :
  1. kr/claude-sonnet-4.5  (Claude 4.5 gratuit Kiro)
  2. kr/glm-5             (GLM-5 gratuit Kiro)
  3. oc/<auto>            (OpenCode Free)

# Maximiser abonnement
premium-coding :
  1. cc/claude-opus-4-6   (abonnement)
  2. glm/glm-5.1          ($0.6/1M backup)
  3. kr/claude-sonnet-4.5 (gratuit urgence)
```

---

## 📊 Tarification réelle

| Tier | Provider | Coût | Reset |
|---|---|---|---|
| Gratuit | Kiro AI | $0 | Illimité |
| Gratuit | OpenCode Free | $0 | Illimité |
| Gratuit | Vertex AI | $300 crédits | 90 jours (nouveau compte GCP) |
| Cheap | GLM-5.1 | $0.6/1M | Journalier |
| Cheap | MiniMax M2.7 | $0.2/1M | Rolling 5h |
| Cheap | Kimi K2.5 | $9/mois flat | 10M tokens/mois |

**9router lui-même est gratuit et open source.** Le dashboard affiche des "coûts estimés" pour montrer les économies réalisées vs API payantes directes — pas une facturation réelle.

---

## ⚠️ Sécurité à garder en tête

- 9router intercepte toutes les requêtes LLM → à faire tourner en local uniquement (`127.0.0.1`)
- Ne jamais exposer le dashboard sur un réseau public sans `REQUIRE_API_KEY=true` et HTTPS
- Les tokens OAuth (Claude Code, Codex) sont stockés localement dans SQLite (`~/.9router/db/data.sqlite`)
- Le mode debug (`ENABLE_REQUEST_LOGS=true`) loggue prompts + réponses — à éviter en prod

---

## 📌 Pertinence pour ce projet

- **Outil clé pour l'IA locale** : normalise Ollama, providers gratuits et abonnements dans une seule interface OpenAI-compatible
- **RTK** : -20-40% tokens input = fenêtre de contexte effective plus grande sur les modèles locaux limités
- **Fallback Ollama** : combiner un modèle local Ollama comme tier 3 gratuit et offline
- **À installer immédiatement** pour maximiser l'abonnement Claude Code Pro actuel en attendant le nouveau Mac
- **Combo recommandé maintenant** : `cc/claude-opus-4-6` (abonnement) → `kr/claude-sonnet-4.5` (gratuit fallback)

**Tags :** `llm-router` · `token-saver` · `claude-code` · `ollama` · `proxy` · `free-ai` · `multi-provider` · `local-ai`
