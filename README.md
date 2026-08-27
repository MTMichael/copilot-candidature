# 🎯 Agent Candidature — Emmanuelle Guei

Suite personnalisée pour **Emmanuelle Guei** — *Assistante de direction · Gestion administration*.

## Ce que fait la suite
- **1 · Agent CV** — génère CV + lettre de motivation adaptés à chaque offre (IA), avec analyse du matching.
- **2 · Tracker** — suivi de toutes les candidatures.
- **3 · Planning** — organisation de la recherche.
- **4 · Recherche** — liens directs vers les plateformes d'emploi, pré-remplis depuis le profil.
- **5 · Match** 🆕 — rapproche ton CV des offres en ligne, filtrées par type de contrat.

## Premier lancement
1. Déplace le dossier sur ton Bureau.
2. Double-clique sur `1-agent-candidature.html` (à ouvrir en premier — ton profil est chargé et partagé avec les autres onglets).
3. **Le profil d'Emmanuelle est déjà pré-rempli** — tu peux générer directement.

## 🎯 Onglet Match
- **Choisis les types de contrat** : Stage, Alternance, CDD, CDI, Intérim (active/désactive chaque contrat d'un clic).
- **Matcher avec des offres en ligne** : l'agent cherche des offres réelles et récentes sur le web et les classe par correspondance avec ton profil (score, points forts, points à renforcer, lien vers l'offre).
- **Recherches directes** : des liens filtrés par contrat (Indeed, Welcome to the Jungle, LinkedIn, HelloWork, France Travail) restent toujours disponibles, même si le matching automatique n'est pas accessible dans ton environnement.

## Mobilité géographique
Dans ⚙ Mon profil ou la carte « Mon profil » : choisis les villes / pays où tu es prête à travailler (pré-rempli : Paris, Île-de-France, Evreux). Case pour l'afficher ou non sur le CV.

## Modifier son profil
**⚙ Mon profil** (barre du haut) ou **✏ Modifier** (bandeau) à tout moment. Le bouton **💾 Enregistrer ces ajouts dans mon profil** conserve les retouches faites dans la carte « Mon profil ».

## Modèle IA
Documents et matching générés avec le modèle Claude actuel (`claude-sonnet-5`).


## 🔧 Nouveautés de cette version
- **Menu harmonisé** sur toutes les pages : mêmes onglets, même ordre (Agent CV → Tracker → Planning → Recherche → Match), bouton **⚙ Mon profil** accessible partout.
- **Générer sans offre** : laisse le champ « Offre d'emploi » vide pour produire un CV général / candidature spontanée basé sur ton profil.
- **Messages d'erreur clairs** : si la génération échoue (« Failed to fetch », clé invalide, quota…), un panneau explique la cause exacte et la marche à suivre.
- **Clé API (usage local)** : sur l'onglet Agent CV, section **🔑 Clé API**, colle ta clé Anthropic pour que la génération fonctionne en double-clic depuis ton Bureau. Elle reste stockée sur ton ordinateur.

## Pourquoi « Failed to fetch » ?
Ouverte en local sans clé, l'application ne peut pas appeler l'IA (le navigateur bloque l'appel). Renseigne ta clé API dans la section 🔑 pour débloquer la génération ; sinon, les onglets Recherche et Match (liens directs) restent utilisables.
