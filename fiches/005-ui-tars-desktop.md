# 🖥️ Fiche #005 — UI-TARS-desktop / Agent TARS (ByteDance)

**Source :** https://github.com/bytedance/UI-TARS-desktop  
**Catégorie :** Agents IA / IA Locale / Computer Use  
**Langage :** TypeScript · Licence : Apache 2.0 · ⭐ 29k · Forks : 2.9k  
**Auteur :** ByteDance  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est

Stack multimodal d'agents IA open source qui livre **deux projets distincts** :

### Agent TARS
Agent multimodal généraliste — CLI + Web UI. Voit l'écran, clique, tape, navigue dans les navigateurs et terminaux via des LLMs multimodaux. S'intègre avec des serveurs MCP pour accéder à des outils du monde réel. Alternative open source à Anthropic Computer Use (payant à l'usage).

### UI-TARS Desktop
Application desktop native pour l'automatisation GUI, pilotée par le modèle UI-TARS (ByteDance) et les modèles Seed-1.5-VL/1.6. Opérateurs local et distant pour computer et browser.

---

## ⚙️ Fonctionnement

**Modes d'action :**
- GUI Agent (visual grounding — le modèle "voit" l'écran)
- DOM (parsing du DOM navigateur)
- Hybride GUI + DOM

**Architecture clé :**
- Kernel construit sur MCP → montage de serveurs MCP pour connecter des outils du monde réel
- Event Stream comme protocole → drive le Context Engineering et l'Agent UI
- Opérateurs local et distant (computer + browser)

**Modèles compatibles :**
- Anthropic Claude (claude-3-7-sonnet-latest)
- Google (Doubao, Gemini)
- Ollama (modèles locaux)
- UI-TARS 1.5 (modèle ByteDance spécialisé GUI)

---

## 🚀 Usage rapide

```bash
# Agent TARS — lancement one-shot
npx @agent-tars/cli@latest

# Avec un provider spécifique
agent-tars --provider anthropic --model claude-3-7-sonnet-latest --apiKey your-api-key
agent-tars --provider volcengine --model doubao-1-5-thinking-vision-pro-250428 --apiKey your-api-key

# Installation globale
npm install @agent-tars/cli@latest -g
```

**UI-TARS Desktop** : application native téléchargeable depuis les releases GitHub.

---

## 📦 Structure du projet

```
UI-TARS-desktop/
├── apps/ui-tars/          # Application desktop native
├── multimodal/            # SDK multimodal
├── packages/              # Packages partagés
├── docs/                  # Documentation et quick-start
└── infra/                 # Infrastructure
```

---

## 🔍 Points notables pour les agents IA locaux

- **Kernel MCP natif** : tout s'intègre via MCP → les serveurs MCP perso peuvent être montés directement
- **Ollama compatible** : peut tourner entièrement en local avec un modèle 7B-70B si le hardware le permet
- **Event Stream** : protocole qui trace chaque action → auditabilité complète de ce que l'agent fait
- **Visual grounding** : le modèle UI-TARS est entraîné spécifiquement pour comprendre les GUIs (pas un LLM générique)
- **Opérateurs distants** : contrôle d'un ordinateur ou navigateur distant sans installation locale

---

## ⚠️ Considérations de sécurité

Un agent qui voit l'écran et clique partout est une surface d'attaque majeure :
- Ne jamais exposer l'opérateur sur un réseau public
- Surveiller les actions via l'Event Stream avant de les valider
- Utiliser des sessions isolées (VM, container) pour les tâches risquées
- Vérifier les permissions accordées aux serveurs MCP montés

---

## 📌 Pertinence pour ce projet

- **Alternative gratuite à Anthropic Computer Use** : même capacité, 0 token facturé si Ollama local
- **Orchestration MCP** : monter ses propres serveurs MCP dans un agent visuel — puissant pour l'automatisation complexe
- **IA locale** : avec UI-TARS 1.5 (7B) + Ollama, pipeline entièrement offline
- **Automatisation de workflows** : tâches répétitives de navigation, extraction de données, tests UI

**Tags :** `computer-use` · `multimodal` · `gui-agent` · `mcp` · `ollama` · `local-ai` · `browser-use`
