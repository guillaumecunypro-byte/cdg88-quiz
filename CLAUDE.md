# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Formation IA Générative d'une journée pour les **Secrétaires de Mairie** du CDG88 (Centre de Gestion des Vosges). Hébergé sur GitHub Pages : `https://guillaumecunypro-byte.github.io/cdg88-quiz/`

## Files

| Fichier | Rôle |
|---------|------|
| `presentation.html` | Présentation formateur — 53 slides (actuellement) |
| `quiz_apprenant.html` | Interface quiz temps réel pour les apprenants (mobile) |
| `index.html` | Page d'accueil hub |
| `house-of-david-poster (1).avif` | Image poster (non utilisée en slide, remplacée par iframe YT) |

## Architecture

### Présentation (`presentation.html`)

HTML statique pur — aucun framework, aucun bundler.

**Structure des slides :**
- Chaque slide est un `<section class="slide [light|dark]" data-slide="N">`
- Le slide actif a la classe `active` — contrôlé par JS via `opacity` et `visibility`
- Navigation : `show(i)`, `next()`, `prev()` — touches clavier ArrowRight/Space/PageDown/Home/End
- `const TOTAL = slides.length` — dynamique, ne pas hardcoder

**Guard clavier (important) :** Le handler `keydown` vérifie `e.target.tagName` pour ne pas changer de slide quand un bouton/input a le focus (cas du quiz interactif).

**CSS Variables (charte CDG88) :**
```css
--navy: #272A5F
--rouge: #E94059
--orange: #F7A720
```

**Structure CSS :** Les slides utilisent `display:flex; flex-direction:column`. Pour centrer verticalement une grille dans un slide, utiliser `align-content:center` (pas seulement `align-items:center` qui centre les items dans leur cellule, pas les lignes dans le conteneur).

**Firebase (quiz intégré au formateur) :**
- SDK compat v10 chargé depuis CDN
- Projet : `formation-ia---fpt` — Realtime Database europe-west1
- Le quiz formateur est intégré en bas de `presentation.html` (slides 50+)

### Structure des slides 12-22 (section IA Générative)

| Slide | Contenu | Type |
|-------|---------|------|
| 12 | 4 types d'IA générative | light |
| 13 | IA Image — 4 outils (DALL·E, Ideogram, Midjourney, Imagen) | light |
| 14 | IA Image — Ifonly influenceur IA (iframe YT `kY35UB6yh5Y`) | light |
| 15 | "Qui est l'artiste ?" — débat | dark |
| 16 | IA Vidéo outils (Sora, KlingAI, Runway + iframe YT `T-8Cr62Nmvs`) | light |
| 17 | Interaction Vidéo deepfake journaliste | dark |
| 18 | House of David — iframe YT `72MxUEfac8U` | light |
| 19 | Emploi — balance menace/opportunité | dark |
| 20 | IA Musique (Suno + Gemini + fausse interface Spotify) | light |
| 21 | Velvet Sundown (groupe IA) | light |
| 22 | Question Spotify — débat | light |
| 23-53 | Suite (éthique, prompting, quiz…) | mixte |

### Classes CSS importantes

- `.s13int-wrap` — grille 2 colonnes pour slides interaction image (15)
- `.sempl-wrap` — grille 2 colonnes pour slides emploi/débat (19, 22)
- `.sfilm-layout` / `.sfilm-left` / `.sfilm-right` — layout House of David (18)
- `.simg-layout` / `.simg-tool` — grille outils image (13)
- `.sifonly-layout` / `.sifonly-video` / `.sifonly-card` — layout Ifonly (14)
- `.svid-layout` — layout IA Vidéo (16)
- `.smus-layout` — layout Musique (20)
- `.svelvet-layout` — layout Velvet Sundown (21)

### Quiz (`quiz_apprenant.html`)

Interface mobile pour les apprenants. Firebase Realtime Database pour la sync formateur ↔ apprenants en temps réel. Les apprenants accèdent via QR code affiché en slide 50+.

## Déploiement

Push sur `main` → GitHub Pages se met à jour automatiquement. Aucun build requis.

## Workflow Git

**Problème récurrent :** L'utilisateur uploade parfois des fichiers directement sur `main` via GitHub, ce qui crée des conflits à chaque PR. Pattern de résolution :
```bash
git checkout --ours presentation.html
git add presentation.html
git commit -m "Merge main, keep our version"
git push
```

Toujours développer sur la branche `claude/charming-hawking-3para2` et créer des PRs vers `main`.

## Compteurs et renommage de slides

Chaque slide a :
1. `data-slide="N"` sur la `<section>`
2. `id="logoN"` sur le `<img class="logo-cdg">`
3. `<div class="slide-counter">N / TOTAL</div>`

Lors d'un renommage en masse, utiliser un script Python avec remplacement max→min pour éviter les collisions. Le TOTAL actuel est **53**.
