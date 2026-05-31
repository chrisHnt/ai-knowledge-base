# 010 — StemDeck

| Champ | Valeur |
|-------|--------|
| **Source** | https://github.com/stemdeckapp/stemdeck |
| **Catégorie** | IA Locale / Audio / Open Source |
| **Langage** | Python 3.10+, JavaScript, Rust (shell Tauri) |
| **Licence** | Apache-2.0 |
| **Date fiche** | 2026-05-31 |
| **Stars** | ~454 |
| **Version** | v0.3.0-alpha.1 (mai 2026) |

---

## Ce que c'est

StemDeck est une application desktop open source de **séparation de stems audio** qui tourne entièrement en local. Elle décompose n'importe quelle piste audio (MP3, WAV, ou URL YouTube) en 6 pistes indépendantes : voix, batterie, basse, guitare, piano, autres. Tout se passe sur la machine de l'utilisateur — aucun upload, aucun compte, aucun abonnement.

Alternative locale gratuite aux services cloud payants type Moises ou LALAL.AI.

---

## Fonctionnement

**Pipeline :**
1. Import audio : drag & drop MP3/WAV ou collage d'URL YouTube (via `yt-dlp`)
2. Séparation via **Demucs `htdemucs_6s`** (réseau de neurones Meta AI, 6 stems)
3. Transcodage et mixage via **FFmpeg**
4. Analyse musicale : BPM + tonalité via **librosa**, loudness LUFS via **pyloudnorm**
5. Lecture dans une interface style **DAW** (waveforms canvas, faders, mute/solo, boucles)

**Accélération GPU :**
- CUDA (NVIDIA) — détection automatique
- MPS (Apple Silicon M1+) — rapide en natif
- CPU fallback — lent mais fonctionnel

**Stack technique :** Python + FastAPI (backend REST + SSE) · Tauri v2 Rust (shell desktop macOS/Windows) · Vanilla JS + Web Audio API (frontend, pas de framework)

**Modèle téléchargé au premier lancement :** ~170 MB (Demucs weights, mis en cache ensuite)

---

## Points notables pour les agents IA locaux

- **Pertinence indirecte pour Jarvis :** StemDeck n'est pas un agent IA, mais son **API REST locale** (`POST /api/jobs`, SSE de progression) est un pattern réutilisable pour piloter de la séparation audio depuis un agent. Un agent Jarvis pourrait appeler cette API pour décomposer un fichier audio avant traitement.
- **Modèle Demucs sous-jacent :** licence MIT, intégrable directement en Python sans passer par StemDeck (`pip install demucs`). Utile si on veut un pipeline audio headless dans un agent.
- **Exécution 100% locale :** aucun cloud, aucune clé API — conforme aux contraintes de Jarvis.
- **Annulation de jobs mid-pipeline :** le runner termine le subprocess actif proprement, pattern intéressant pour des agents avec timeout.
- **Docker supporté :** déploiement conteneurisé possible (sans passthrough GPU sur macOS Docker).

---

## Usage rapide

```bash
# Clone + démarrage (macOS/Linux)
git clone https://github.com/stemdeckapp/stemdeck stemdeck && cd stemdeck
./run.sh setup   # installe ffmpeg, uv, dépendances
./run.sh start   # lance sur http://localhost:8000
```

```bash
# Docker
docker compose -f build/docker-compose.yml up --build
# Stems dans ./jobs/ sur l'hôte
```

**Appel API (exemple) :**
```bash
# Soumettre un fichier audio
curl -X POST http://localhost:8000/api/jobs \
  -H 'Content-Type: application/json' \
  -d '{"url": "https://youtube.com/watch?v=...", "stems": ["vocals", "drums"]}'

# Suivre la progression (SSE)
curl http://localhost:8000/api/jobs/{id}/events

# Télécharger un stem
curl http://localhost:8000/api/jobs/{id}/stems/vocals.wav -o vocals.wav
```

---

## Honnêteté sur les limites

Le README de StemDeck est transparent sur ses limites vs les solutions commerciales :

| Critère | StemDeck | Moises/LALAL.AI |
|---------|----------|-----------------|
| Prix | Gratuit | Freemium/abonnement |
| Qualité séparation | Correcte (Demucs htdemucs_6s) | Supérieure (modèles proprio) |
| Vitesse | Dépend du GPU local | Rapide (cloud) |
| Batch | Non (1 job à la fois) | Oui (plans payants) |
| Mobile | Non | iOS/Android |
| Vie privée | Audio jamais transmis | Upload obligatoire |

> Note : le modèle piano de `htdemucs_6s` est reconnu comme imparfait dans la doc officielle de Demucs.

---

## Pertinence pour ce projet

**Usage direct :** Faible pour Jarvis en tant qu'agent conversationnel, mais **pertinent pour un pipeline audio local** — notamment en lien avec les explorations voix/musique (VoxCPM2, Suno, RVC).

**Usage indirect :** Le pattern API REST locale + SSE de StemDeck est un bon exemple d'outil lourd (ML) exposé proprement comme microservice, pilotable par un agent. À garder comme référence d'architecture.

**Demucs seul** (sans StemDeck) est plus pertinent si on veut intégrer la séparation dans un pipeline Jarvis headless.
