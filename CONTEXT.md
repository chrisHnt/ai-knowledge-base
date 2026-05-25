# Contexte — AI Knowledge Base

## Repos GitHub

### → AI Knowledge Base (ce repo)
- Owner : chrisHnt
- Repo : ai-knowledge-base
- URL : https://github.com/chrisHnt/ai-knowledge-base
- Sujet : tout ce qui touche à l'IA (LLMs, agents, RAG, MCP/A2A, IA locale, sécurité IA…)

### → Tech Knowledge Base (repo sœur)
- Owner : chrisHnt
- Repo : tech-knowledge-base
- URL : https://github.com/chrisHnt/tech-knowledge-base
- Sujet : outils tech hors IA (CLI, DevOps, productivité, sécurité générale, data, design…)

## Règles de dispatch automatique

Quand une liste de liens est partagée, chaque lien est analysé individuellement et redirigé vers le bon repo.

### → ai-knowledge-base
Tout ce qui touche à : LLMs, agents IA, RAG, embeddings, fine-tuning, IA locale, protocoles MCP/A2A, orchestration IA, sécurité IA, frameworks d'agents.

### → tech-knowledge-base
Tout ce qui ne concerne pas l'IA : dev tools, CLI, infra, DevOps, monitoring, data, productivité, utilitaires, sécurité générale, design, scripting.

### Cas ambigus
Si un outil est à cheval (ex. monitoring utilisable aussi pour agents IA), signaler le doute à l'utilisateur et choisir le repo le plus pertinent par défaut.

## Workflow
Quand l'utilisateur partage un lien ou une liste de liens :
1. Fetcher le contenu de chaque page
2. Classifier : IA → ai-knowledge-base / Tech → tech-knowledge-base
3. Produire une fiche structurée (voir format ci-dessous)
4. Créer le fichier `fiches/00X-nom.md` dans le bon repo
5. Mettre à jour l'index dans `README.md` du bon repo

## Format d'une fiche (AI KB)
- Numéro séquentiel (001, 002…)
- Titre, source, catégorie, langage, licence, date
- Ce que c'est (résumé)
- Fonctionnement
- Points notables pour les agents IA locaux
- Usage rapide (si applicable)
- Pertinence pour ce projet

## Catégories (AI KB)
- Sécurité
- Agents IA
- IA Locale
- Protocoles (MCP, A2A…)
- Open Source
