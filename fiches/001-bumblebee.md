# 🔐 Fiche #001 — Bumblebee (perplexityai)

**Source :** https://github.com/perplexityai/bumblebee  
**Catégorie :** Sécurité / Supply-chain / Inventaire d'environnement dev  
**Langage :** Go · Licence : Apache 2.0 · v0.1.1 (mai 2026) · ⭐ 1.7k  
**Date d'ajout :** 2026-05-24

---

## 🧠 Ce que c'est
Scanner read-only d'endpoints développeur (macOS/Linux). Inspecte les métadonnées sur disque — lockfiles, manifestes d'extensions, configs MCP — pour répondre à une question précise lors d'un incident supply-chain : **quelles machines ont ce package compromis installé en ce moment ?**

Complète les SBOMs (ce qui a été livré) et les EDR (ce qui a tourné réseau), en couvrant l'état local "sale" des machines dev.

---

## ⚙️ Fonctionnement
- Binaire statique unique (zéro dépendances non-stdlib)
- 3 profils de scan :
  - `baseline` — inventaire léger global (extensions, toolchains, MCP)
  - `project` — répertoires de développement configurés
  - `deep` — scan à la demande sur un path explicite (ex: `$HOME`)
- Sortie : NDJSON (un record par ligne) → pipeable vers n'importe quel système
- Pas d'exécution de package managers, lecture disque uniquement

---

## 📦 Écosystèmes couverts
npm · pnpm · Yarn · Bun · PyPI · Go modules · RubyGems · Composer · **configs MCP** (`claude_desktop_config.json`, `mcp.json`, `cline_mcp_settings.json`, `~/.gemini/settings.json`…) · Extensions VS Code/Cursor/Windsurf · Extensions navigateurs (Chromium, Firefox)

---

## 🔍 Point notable pour les agents IA locaux
Bumblebee parse les configs MCP pour inventorier les serveurs déclarés, mais n'émet pas les valeurs d'env (credentials). Outil de référence pour auditer quels serveurs MCP sont configurés sur une machine dev, et détecter une dépendance compromise dans la chaîne d'outils d'un agent local.

---

## 🚀 Usage rapide
```bash
# Inventaire global
bumblebee scan --profile baseline > inventory.ndjson

# Vérification d'exposition sur advisory connu
bumblebee scan --profile deep \
  --root "$HOME" \
  --exposure-catalog ./catalog.json \
  --findings-only
```

---

## 📌 Pertinence pour ce projet
- **Sécurité des agents locaux** : auditer les configs MCP, détecter les packages compromis
- **Supply-chain** : surface d'attaque d'un setup dev local
- **À utiliser** si tu déploies des agents avec des serveurs MCP — scanner les configs avant production
