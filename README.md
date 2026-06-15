# Formation IA Générative — CDG88 2026

Formation d'une journée destinée aux **Secrétaires de Mairie** des Vosges, animée par le Centre de Gestion 88.

## Fichiers

| Fichier | Usage | Public |
|---|---|---|
| `index.html` | Page d'accueil — hub de la formation | Formateur |
| `presentation.html` | Présentation complète (41 slides) | Formateur (grand écran) |
| `quiz_apprenant.html` | Quiz interactif temps réel | Apprenants (mobile) |

## Programme de la journée

| Horaire | Contenu |
|---|---|
| 9h00 — 10h30 | Comprendre l'IA — Acculturation |
| 10h30 — 10h45 | ☕ Pause |
| 10h45 — 12h30 | Prompts & Découverte des outils |
| 12h30 — 13h30 | 🍽️ Déjeuner |
| 13h30 — 15h30 | Cas d'usages en groupes |
| 15h30 — 16h00 | Conclusion & Hallucinations |

## Thèmes abordés

- **Acculturation** : histoire de l'IA (1945 → aujourd'hui), usage quotidien sans le savoir
- **Outils** : ChatGPT, Gemini, Claude, Le Chat (Mistral 🇫🇷), Perplexity
- **Prompting** : framework RCTF (Rôle · Contexte · Tâche · Format)
- **Éthique** : hallucinations, propriété intellectuelle, shadow IA, règle des 3C
- **Réglementation** : AI Act européen
- **Pratique** : exercices sur cas réels de commune
- **Quiz final** : 10 questions Kahoot-style avec podium

## Déploiement

Les fichiers sont en HTML statique pur — aucun serveur requis. Ouvrir `index.html` directement dans un navigateur, ou déployer sur GitHub Pages / tout hébergeur statique.

Le quiz utilise **Firebase Realtime Database** pour la synchronisation formateur ↔ apprenants en temps réel.
