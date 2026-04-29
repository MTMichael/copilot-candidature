# COPILOT — Agent IA de candidature

> Un assistant complet pour structurer ta recherche d'emploi : génération de CV et lettres de motivation adaptés à chaque offre, suivi des candidatures, planning chronométré de 2 h par jour, et accès rapide à 25+ plateformes d'offres.

**Auteur :** Michael MWEPA
**Stack :** HTML / CSS / Vanilla JS — 4 fichiers autonomes, aucun build, aucun serveur
**IA :** API Anthropic (Claude) ou Claude.ai (au choix de l'utilisateur)

---

## 🎯 Pourquoi ce projet

Je suis passionné par l'intelligence artificielle et plus particulièrement par les **agents IA** — ces systèmes capables d'orchestrer plusieurs étapes pour accomplir une tâche complète plutôt que de répondre ponctuellement à une question. COPILOT est ma façon de mettre cette passion au service d'un problème concret que tout le monde finit par rencontrer : **chercher un emploi de manière structurée, sans s'épuiser ni s'éparpiller**.

Plutôt que de construire un énième chatbot, j'ai voulu un agent qui :
- *prend en charge tout le cycle de candidature* (recherche → génération → envoi → suivi → relance)
- *garde l'humain au centre* — c'est l'utilisateur qui décide, l'IA rédige et structure
- *fonctionne offline-first* — toutes les données restent dans le navigateur (`localStorage`), rien n'est envoyé à un serveur tiers
- *reste décliné facilement* — la même architecture s'adapte à d'autres métiers (immobilier, vente, freelance, etc.)

L'objectif n'est pas de "remplacer le chercheur d'emploi par l'IA" mais de **lui donner un copilote** qui automatise le formatage, la structure, le matching de mots-clés et le suivi — pour qu'il garde son énergie pour ce qui compte : convaincre, rencontrer, négocier.

---

## 🧩 Les 4 modules

### 1. `1-agent-candidature.html` — Agent CV + Lettre de motivation
- Wizard de configuration en 3 étapes (identité, parcours, métiers visés)
- Score de matching offre ↔ profil avec mots-clés détectés
- Génération CV adapté + LM personnalisée selon la structure définie par l'utilisateur
- Choix entre Claude.ai (copier-coller le prompt) ou API Anthropic (clé saisie une fois, stockée localement)
- Export en HTML / Markdown / texte brut

### 2. `2-tracker.html` — Tracker de candidatures
- Tableau interactif de toutes les candidatures (poste, entreprise, statut, relance prévue)
- Filtres par statut et type de contrat
- Modale d'ajout / édition avec calcul automatique de la date de relance (J+7)
- Export CSV ou JSON, plus un script Apps Script prêt à coller dans Google Sheets

### 3. `3-planning.html` — Planning 2 h par jour
- Chronomètre de session avec notification à 2 h atteintes
- Plan de session recommandé (5 blocs : sourcing, génération, envoi, relances, réseau)
- Objectifs du jour avec checklist
- Vue semaine avec streak (jours consécutifs)
- Citations motivantes en rotation

### 4. `4-recherche.html` — 25+ plateformes d'offres
- Génération de liens pré-remplis selon métier, secteur, localisation, contrat
- Recommandations contextuelles (★ marquage des plateformes pertinentes selon ton profil et type de contrat)
- Raccourcis par métier (marketing, dev, design, freelance, stage, etc.)
- Stratégie hybride : URL directe quand le pattern est stable, sinon recherche Google `site:domain.com` (toujours fonctionnelle)

---

## ⚙ Installation & utilisation

Pas d'installation. Ce sont 4 fichiers HTML statiques.

```bash
# Cloner ou télécharger les fichiers
git clone https://github.com/<ton-repo>/copilot.git
cd copilot

# Ouvrir directement dans le navigateur
open 1-agent-candidature.html
```

**Au premier lancement**, le wizard de configuration s'affiche. Renseigne ton parcours, sauvegarde, et tu peux commencer.

**Pour utiliser l'IA**, deux modes au choix :

1. **Mode Artifact (Claude.ai)** : ouvre l'agent directement dans Claude.ai en tant qu'Artifact → laisse le champ "Clé API" vide, ça marche direct.
2. **Mode local (fichier HTML)** : ouvre le `.html` depuis ton navigateur → colle ta clé API Anthropic dans le wizard. Elle est stockée en local, jamais transmise ailleurs.

Tu peux créer ta clé API gratuitement ici : [console.anthropic.com](https://console.anthropic.com/settings/keys).

Alternative sans clé API : copie-colle manuellement les prompts générés dans [claude.ai](https://claude.ai), récupère la réponse, recolle dans l'agent.

---

## 🔒 Confidentialité et données

Toutes tes données restent dans ton navigateur (`localStorage`). Aucun serveur, aucun tracking, aucune analytics.

Si tu utilises l'API Anthropic, le contenu de tes candidatures transite par Anthropic au moment de la génération — c'est inhérent à l'utilisation d'une API IA. La clé API est stockée en local et n'est jamais envoyée ailleurs.

Pour effacer toutes tes données : `Paramètres du navigateur → Effacer les données du site`.

---

## 🛠 Architecture technique

```
copilot/
├── 1-agent-candidature.html    # CV + LM (~1500 lignes, JS 800)
├── 2-tracker.html              # Tracker (~770 lignes, JS 350)
├── 3-planning.html             # Planning 2h (~580 lignes, JS 250)
└── 4-recherche.html            # Recherche multi-plateformes (~600 lignes, JS 450)
```

**Choix techniques :**
- Vanilla JS uniquement (pas de framework, pas de build, pas de package.json)
- Polices Google Fonts : Cormorant Garamond (titres) + DM Sans (texte)
- Palette unique partagée par les 4 fichiers (variables CSS `--accent`, `--gold`, etc.)
- Stockage : `localStorage` (pas d'IndexedDB, pas de cookies)
- Aucune dépendance externe runtime hormis les CDN polices

**Pourquoi pas de framework ?** Parce que pour 4 pages avec quelques centaines de lignes de logique, React/Vue ajoutent plus de complexité qu'ils n'en retirent. Et parce que ce projet doit pouvoir être ouvert dans 5 ans sans dépendre d'un écosystème npm qui aura changé 12 fois entre temps.

---

## 🧠 Le pattern à retenir

Ce qui rend COPILOT déclinable à d'autres métiers, c'est le pattern de fond — pas le code spécifique :

```
PROFIL utilisateur
  └─→ CONTEXTE (offre, situation, données entrantes)
        └─→ SCORING / ANALYSE par l'IA
              └─→ DOCUMENT / ACTION générée
                    └─→ SUIVI structuré
```

Ce même squelette peut faire un **agent prospection commerciale** (profil = ton entreprise, contexte = un prospect, scoring = matching, doc = email perso, suivi = CRM), un **agent immobilier** (profil = ton bien, contexte = un locataire, scoring = compatibilité, doc = annonce + dossier, suivi = visites), un **agent freelance** (profil = ton offre, contexte = une mission Malt, scoring = adéquation, doc = proposition, suivi = pipeline)...

C'est pour ça que je m'intéresse aux agents IA : **un seul pattern bien pensé débloque dix cas d'usage**.

---

## 📋 Roadmap

- [ ] Mode mobile complet (déjà responsive, mais des affinements à faire)
- [ ] Intégration directe avec Google Calendar pour le bloc 2h
- [ ] Mode "agence" : gérer plusieurs profils dans le même navigateur
- [ ] Versions déclinées : *Prospection commerciale*, *Recherche locataire*, *Recherche stage*
- [ ] Export du dossier complet en ZIP (CV PDF + LM + tracker CSV)
- [ ] Plugin Chrome pour ajouter une candidature en 1 clic depuis n'importe quel jobboard

---

## 🤝 Réutiliser & adapter

Le code est volontairement simple pour pouvoir être lu et modifié sans connaissance préalable d'un framework. Si tu veux décliner COPILOT pour un autre métier, le plus simple est de :

1. Récupère le code (Download ZIP, clone Git, ou *fork* sur GitHub si tu connais)
2. Modifie les *prompts* dans `1-agent-candidature.html` (variables `PROMPT_CV`, `PROMPT_LM`, `PROMPT_SCORE`)
3. Adapte les listes de plateformes dans `4-recherche.html` (`PF_GEN`, `PF_CADRES`, etc.)
4. Garde le reste tel quel — la structure tient

---

## 📬 Contact

**Michael MWEPA**
Passionné d'IA, d'agents intelligents et de produits qui ont du sens.

LinkedIn : [à compléter]
Email : [à compléter]

---

*Conçu avec rigueur, livré avec sincérité. COPILOT n'est pas magique — c'est juste un bon copilote.*
