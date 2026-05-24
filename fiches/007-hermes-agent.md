# ⚗️ Fiche #007 — hermes-agent (NousResearch)

**Source :** https://github.com/NousResearch/hermes-agent  
**Catégorie :** Agents IA / IA Locale / Framework agent complet  
**Langage :** Python 88% · Licence : MIT · ⭐ 156k · Forks : 25k  
**Auteur :** Nous Research  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Framework d'agent IA complet et auto-améliorant, conçu par Nous Research (lab IA spécialisé dans les LLMs open source). L'agent peut tourner sur n'importe quel provider (Ollama local, OpenRouter, Anthropic, OpenAI…) et se distingue par **une boucle d'apprentissage intégrée** : il crée des skills à partir de son expérience, les améliore en cours d'utilisation, et construit un modèle persistant de l'utilisateur au fil des sessions.

**Tagline** : *"The agent that grows with you"*

---

## ⚙️ Fonctionnement

### Boucle d'apprentissage fermée
- Création autonome de skills après des tâches complexes
- Auto-amélioration des skills pendant l'utilisation
- Mémoire persistante avec nudges périodiques pour persister la connaissance
- Recherche full-text (FTS5) sur les sessions passées avec résumé LLM
- Modélisation utilisateur dialectique via [Honcho](https://github.com/plastic-labs/honcho)

### Providers supportés
Nous Portal, OpenRouter (200+ modèles), NovitaAI, NVIDIA NIM, Ollama, Hugging Face, OpenAI, Anthropic, Kimi, MiniMax, xAI, Mistral, Groq… Switch via `hermes model` sans modifier le code.

### Backends terminal (7)
| Backend | Usage |
|---|---|
| Local | Défaut, machine courante |
| Docker | Isolation container |
| SSH | Machine distante |
| Singularity | HPC/cluster |
| Modal | Serverless, hibernation, wake on demand |
| Daytona | Persistance serverless |
| Vercel Sandbox | Edge |

### Multi-plateforme messaging
Telegram, Discord, Slack, WhatsApp, Signal, Email — un seul processus gateway.

---

## 🚀 Installation

```bash
# Linux / macOS / WSL2 / Termux
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
source ~/.bashrc
hermes              # démarrer

# Windows (PowerShell, beta)
irm https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.ps1 | iex

# Depuis les sources
git clone https://github.com/NousResearch/hermes-agent.git
cd hermes-agent && ./setup-hermes.sh
./hermes
```

### Commandes principales
```bash
hermes              # CLI interactif
hermes model        # Choisir provider + modèle
hermes tools        # Configurer les outils activés
hermes gateway      # Démarrer le gateway messaging
hermes setup        # Assistant de configuration complet
hermes update       # Mettre à jour
hermes doctor       # Diagnostiquer les problèmes
hermes claw migrate # Migrer depuis OpenClaw
```

---

## 🗂️ Capacités clés

| Capacité | Détail |
|---|---|
| **Learning loop** | Skill creation autonome + auto-amélioration |
| **Mémoire persistante** | Agent-curated + FTS5 search + user modeling (Honcho) |
| **Skills system** | Compatible [agentskills.io](https://agentskills.io) standard ouvert |
| **MCP integration** | Montage de serveurs MCP pour étendre les capacités |
| **Cron scheduler** | Tâches planifiées en langage naturel + livraison multi-plateforme |
| **Subagents** | Spawn d'agents isolés pour travaux parallèles |
| **Python RPC tools** | Scripts Python appelant des outils via RPC |
| **Transcription voix** | Mémos vocaux transcrits, continuité cross-plateforme |
| **Research-ready** | Génération batch de trajectoires pour fine-tuning |

---

## 📱 Accès distant (aspect IA locale)

Hermes n'est pas lié à une machine locale. Cas d'usage typique :
- Tourner l'agent sur un VPS à 5$/mois
- Lui parler depuis Telegram quand il travaille sur une VM cloud
- Backends Modal/Daytona : l'environnement hiberne quand inactif, se réveille à la demande

```bash
# Exemple : agent sur GPU cloud, interface Telegram
hermes gateway setup  # configurer Telegram bot token
hermes gateway start  # démarrer le gateway
# Envoyer un message au bot depuis Telegram → l'agent répond et agit
```

---

## 🔍 Intégration MCP

Hermes supporte les serveurs MCP comme source d'outils. Configuration dans `~/.hermes/config.yaml` :

```yaml
mcp_servers:
  agentmemory:
    command: npx
    args: ["-y", "@agentmemory/mcp"]
  mon_serveur:
    command: python
    args: ["mon_serveur_mcp.py"]
```

Compatibilité native avec agentmemory (fiche #006) pour la mémoire persistante.

---

## ⚠️ Limites / Points d'attention

- **Très gros repo** (156k stars, 8700+ commits) → écosystème actif mais complexe
- **Windows natif en beta** : WSL2 recommandé pour usage sérieux
- **Python-first** : moins adapté si ton stack est entièrement TypeScript/Node
- **Courbe d'apprentissage** sur la configuration gateway et les toolsets

---

## 📌 Pertinence pour ce projet

- **Référence #1 pour les agents locaux** sur modèles 7B-34B via Ollama : `hermes model` → sélectionner Ollama → choisir le modèle
- **Learning loop** : l'agent qui s'améliore seul est le modèle cible pour l'orchestration autonome
- **MCP natif** : connecter ses propres serveurs MCP directement
- **Migration OpenClaw** : si tu utilises OpenClaw, migration en une commande
- **À tester en priorité** quand le nouveau Mac arrive avec Ollama + un modèle 7B-34B

**Tags :** `local-ai` · `ollama` · `agent-framework` · `mcp` · `memory` · `skills` · `self-improving` · `telegram`
