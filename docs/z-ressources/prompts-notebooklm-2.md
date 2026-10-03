---
title: Prompts NotebookLM pour l'enseignement (maths / NSI) et l'usage perso
description: Bibliothèque de prompts prêts à copier-coller pour NotebookLM, classés par usage.
---

# Prompts NotebookLM : enseignant, élèves, perso

Bibliothèque de prompts à copier-coller dans [NotebookLM](https://notebooklm.google.com). Ils sont adaptés du guide de prompts « Gemini Notebook » et réécrits en français pour l'enseignement des **mathématiques** et de la **NSI** au lycée.

## Mode d'emploi

NotebookLM répond **uniquement à partir des sources que tu charges** dans le carnet (PDF, Google Docs, pages web, vidéos YouTube, audio…). Les réponses sont accompagnées de citations cliquables, ce qui permet de vérifier.

- Remplace tout ce qui est entre `[CROCHETS]` par tes propres informations.
- Ajoute dans le carnet les bonnes sources : programme officiel, tes cours, manuels, sujets d'examen, notices, contrats…
- Un carnet par thème fonctionne mieux qu'un carnet fourre-tout (par exemple « NSI Première », « Grand oral », « Maison »).
- Vérifie toujours les formules, le code et les corrigés générés. Le LaTeX et l'indentation du code Python sont parfois mal repris.
- **RGPD** : ne charge jamais de données nominatives d'élèves (notes, appréciations, dossiers) dans un carnet.

!!! tip "Astuce"

    Termine un prompt par « Cite tes sources » ou « Indique le passage exact » pour forcer les citations, et par « Si l'information n'est pas dans les sources, dis-le clairement » pour limiter les inventions.

## Vue d'ensemble

| Prompt | Enseignant | Élèves | Perso |
|---|:---:|:---:|:---:|
| Synthèse des sources | ✅ | ✅ | ✅ |
| Extraction de preuves | ✅ | ✅ | ✅ |
| Détection des contradictions | ✅ | ✅ | ✅ |
| Analyse des lacunes | ✅ | ✅ | ✅ |
| Points de vue alternatifs | ✅ | ✅ | ✅ |
| Rédaction de contenu | ✅ | ✅ | ✅ |
| Guide de référence structuré | ✅ | ✅ | ✅ |
| Réunions et actions | ✅ | | ✅ |
| Notices, pannes, garanties | | | ✅ |

---

# 1. Enseignant

## 1.1 Veille et recherche

### Synthèse des sources

```text
Fais la synthèse des thèmes principaux de toutes les sources de ce carnet. Donne les 3 à 5 points essentiels à retenir, indique sur quels points les sources s'accordent le plus et quels points sont traités différemment. Cite tes sources.
```

### Extraction de preuves (version programme officiel)

```text
Dans ces sources, où apparaissent les contenus et capacités attendues sur [NOTION : récursivité / bases de données / suites numériques / probabilités conditionnelles] ? Cite les passages exacts, avec le document d'origine et le niveau concerné.
```

### Extraction de preuves (version argumentaire)

```text
À partir de ces sources, quels sont les éléments les plus solides en faveur de [AFFIRMATION OU ANGLE, par exemple « la programmation par projet améliore la motivation des élèves »] ? Cite chaque source pour que je puisse vérifier, et signale si les preuves sont faibles ou indirectes.
```

### Détection des contradictions

```text
En te basant uniquement sur les sources de ce carnet, identifie les points où elles se contredisent ou divergent : définitions, notations, méthodes, conventions, vocabulaire, ordre de présentation. Pour chaque désaccord, cite les deux passages concernés.
```

### Analyse des lacunes

```text
D'après ces sources, quelles questions ou sous-thèmes importants sont absents ou à peine traités à propos de [SUJET] ? Liste les principales lacunes qu'il faudrait combler, de la plus importante à la moins importante.
```

### Points de vue alternatifs

```text
Existe-t-il des points de vue minoritaires, contradictoires ou peu connus sur [SUJET, par exemple « l'usage de l'IA générative en cours d'informatique »] qui ne sont probablement pas représentés dans ces sources ? Décris-les en quelques lignes chacun et indique quel type de source je devrais ajouter pour les couvrir.
```

## 1.2 Préparation des cours

### Comparer ma progression au programme

```text
Compare ma progression annuelle avec le programme officiel de [NIVEAU ET ENSEIGNEMENT, par exemple « première NSI »]. Présente un tableau avec : les capacités attendues, où je les travaille dans ma progression, et celles qui sont absentes ou peu travaillées. Cite le programme.
```

### Fiche de cours

```text
À partir uniquement de ces sources, rédige une fiche de cours sur [NOTION] pour des élèves de [NIVEAU]. Structure : définitions, propriétés ou algorithmes à retenir, exemple commenté, erreurs fréquentes. Utilise un langage clair et des phrases courtes. Écris les formules en LaTeX.
```

### Exercices progressifs avec corrigé

```text
À partir uniquement de ces sources, rédige 5 exercices progressifs sur [NOTION] pour des élèves de [NIVEAU] : le premier d'application directe, le dernier demandant de l'initiative. Donne le corrigé détaillé de chacun, puis indique la capacité du programme travaillée.
```

### Activité débranchée ou TP guidé (NSI)

```text
À partir de ces sources, propose un TP guidé de [DURÉE] sur [NOTION NSI] en Python. Donne : les objectifs, les prérequis, un énoncé avec des questions progressives, un code de départ à compléter, le corrigé commenté, et les difficultés prévisibles des élèves.
```

### Projet NSI

```text
À partir de ces sources, propose 5 idées de projets pour des élèves de [NIVEAU], réalisables en [DURÉE] par groupes de [NOMBRE]. Pour chaque projet : objectif, notions du programme mobilisées, étapes de travail, livrables attendus et critères d'évaluation.
```

### Sujet d'évaluation avec barème

```text
Rédige un devoir surveillé de [DURÉE] sur [CHAPITRES], niveau [NIVEAU], à partir des sources de ce carnet. Inclure : 3 à 4 exercices de difficulté croissante, un barème sur [TOTAL] points, un corrigé détaillé et une liste des erreurs typiques à surveiller en correction.
```

### Différenciation

```text
À partir de cet exercice ou de cette activité [COLLER OU INDIQUER LA SOURCE], propose trois variantes : une version avec coups de pouce pour les élèves en difficulté, une version standard et une version d'approfondissement. Garde les mêmes objectifs d'apprentissage.
```

### Diagnostic des erreurs fréquentes

```text
D'après ces sources, quelles sont les erreurs et les conceptions erronées les plus fréquentes des élèves à propos de [NOTION] ? Pour chacune, explique l'origine probable et propose une question ou un contre-exemple qui permet de la faire émerger en classe.
```

## 1.3 Réunions et suivi de projets

!!! warning "Données personnelles"

    N'importe que des comptes rendus anonymisés, sans noms ni situations d'élèves.

### Gestion des actions

```text
Dans toutes les réunions de ce carnet, liste toutes les actions qui ont été attribuées. Pour chacune, indique : la personne responsable, l'échéance si elle est mentionnée, la réunion d'origine, et son statut apparent (fait, en cours, non mentionné).
```

### Décisions prises

```text
Quelles sont les décisions prises lors de ces réunions ? Liste-les par ordre chronologique, avec la réunion d'origine pour chacune.
```

### Ordre du jour de la prochaine réunion

```text
À partir des actions et des questions ouvertes de la dernière réunion, propose un ordre du jour pour la prochaine réunion. Inclus les points à suivre, les décisions à prendre et une durée estimée pour chaque point.
```

## 1.4 Communication

### Message aux familles

```text
Résume en 150 mots maximum le contenu principal de ce carnet pour un message aux parents. Commence par l'information la plus importante ou la plus actionnable, utilise un ton bienveillant et sans jargon, et termine par ce qui est attendu des familles.
```

### Texte à partir d'une vidéo ou d'une conférence

```text
À partir de la transcription de ce carnet, propose un plan détaillé de polycopié pour des lecteurs (et non des spectateurs). Réorganise le contenu, enlève les redites orales, ajoute des intertitres et signale les passages qui nécessiteraient un schéma ou un exemple supplémentaire.
```

## 1.5 Guide de référence structuré

Un prompt qui impose une structure fixe. Il donne des documents homogènes, faciles à publier sur un site ou à imprimer. Il s'applique à un carnet qui contient plusieurs sources sur **un même sujet** (documentation, cours, notices).

### Version avancée

```text
À partir de toutes les sources chargées, produis un guide de référence sur [SUJET] au format Markdown strict.

Structure imposée :
# Titre principal
## Description
## Comparaison (tableau si pertinent)
## Commandes ou protocoles types (blocs de code si technique, sinon étapes standards)
## Bonnes pratiques
## Pièges connus et solutions

Contraintes : niveau avancé, français formel, aucun émoji, aucun avertissement générique. Utilise exclusivement les sources, sans connaissance extérieure. Si une section ne peut pas être remplie avec les sources, écris « Non couvert par les sources » au lieu de l'inventer. Cite la source de chaque point important.
```

### Version lycée (cours, fiche à distribuer)

```text
À partir de toutes les sources chargées, produis une fiche de référence sur [NOTION] pour des élèves de [NIVEAU], au format Markdown strict.

Structure imposée :
# Titre
## L'essentiel en 5 lignes
## Définitions et notations
## Méthodes ou algorithmes (avec un exemple traité pas à pas)
## Exemples de code ou de calculs (blocs de code ; formules en LaTeX)
## Erreurs fréquentes
## Pour s'entraîner (3 questions, sans corrigé)

Contraintes : tutoiement, vocabulaire du programme, phrases courtes, aucun émoji. Utilise exclusivement les sources du carnet. Si un point n'est pas dans les sources, ne l'invente pas : signale-le.
```

### Version perso (appareil, logiciel, démarche)

```text
À partir de toutes les sources chargées, produis un mémo sur [SUJET : un appareil, un logiciel, une démarche administrative] au format Markdown strict.

Structure imposée :
# Titre
## À quoi ça sert
## Réglages ou informations clés (tableau)
## Procédures courantes (étapes numérotées)
## Entretien ou échéances à ne pas oublier
## Problèmes connus et solutions

Contraintes : français clair, aucun émoji. Utilise exclusivement les sources. Indique la page ou la section d'origine pour chaque procédure.
```

!!! note "Pourquoi « Non couvert par les sources »"

    Un prompt qui impose une structure complète pousse le modèle à remplir chaque section, même quand les sources n'ont rien à dire. Autoriser explicitement le vide évite le remplissage et les inventions.

---

# 2. Élèves

!!! info "À donner en classe"

    Ces prompts peuvent être distribués tels quels. Rappelle aux élèves de charger **le cours de la classe**, pas des sources trouvées au hasard, et de comparer la réponse avec leur cahier.

## 2.1 Révision

### Résumé du chapitre

```text
À partir uniquement des sources de ce carnet, fais-moi une fiche de révision sur [CHAPITRE] pour un élève de [NIVEAU]. Donne : les définitions à connaître par cœur, les propriétés ou méthodes essentielles, un exemple type et les 3 erreurs les plus fréquentes.
```

### Ce que je dois savoir pour le contrôle

```text
Je prépare un contrôle sur [CHAPITRES]. D'après mes sources, liste ce qui est le plus important à maîtriser, du plus essentiel au plus secondaire. Pour chaque point, indique où je peux le retrouver dans mes documents.
```

### Interroge-moi

```text
Pose-moi un quiz de 10 questions sur [CHAPITRE], une question à la fois, en commençant par les plus faciles. Attends ma réponse avant de passer à la suivante, corrige-moi, explique mes erreurs en citant mon cours, puis donne mon score à la fin.
```

### Flashcards

```text
Crée 15 cartes de révision sur [CHAPITRE] à partir de mes sources. Pour chaque carte : une question courte (définition, propriété, syntaxe Python, résultat à connaître) et une réponse courte. Présente le tout sous forme de tableau.
```

### Explique-moi autrement

```text
Je n'ai pas compris [NOTION] dans mon cours. Explique-la avec des mots simples et un exemple concret, à partir de mes sources uniquement. Puis pose-moi une question pour vérifier que j'ai compris.
```

### Exercices d'entraînement avec correction à part

```text
Propose-moi 5 exercices d'entraînement sur [NOTION], de difficulté croissante, à partir de mes sources. Donne uniquement les énoncés. Je te donnerai mes réponses ensuite et tu me les corrigeras.
```

### Correction de ma réponse

```text
Voici ma réponse à l'exercice : [COLLER L'ÉNONCÉ ET TA RÉPONSE]. Dis-moi si elle est correcte. Si non, indique à quelle ligne se situe l'erreur et donne un indice sans me donner directement la solution.
```

### Débogage guidé (NSI)

```text
Voici mon code Python et le message d'erreur que j'obtiens : [COLLER LE CODE ET L'ERREUR]. Ne me donne pas directement le code corrigé. Explique-moi d'abord ce que signifie l'erreur, aide-moi à repérer la ligne en cause et propose-moi une piste à tester.
```

### Plan de révision

```text
J'ai un contrôle le [DATE] sur [CHAPITRES] et je peux travailler [DURÉE] par jour. À partir de mes sources, construis-moi un planning de révision jour par jour, avec pour chaque séance : ce qu'il faut relire, ce qu'il faut refaire et un mini-test final.
```

### Lacunes dans mes révisions

```text
D'après mes sources, quelles notions de [CHAPITRE] sont peu couvertes dans mes fiches ou mes exercices par rapport au cours ? Dis-moi sur quoi je devrais encore m'entraîner.
```

## 2.2 Tutorat

### Pour l'élève tuteur : préparer une séance

```text
Je dois aider un camarade de [NIVEAU] qui n'a pas compris [NOTION]. À partir de ces sources, aide-moi à préparer une séance de 30 minutes : 2 ou 3 questions pour repérer ce qu'il n'a pas compris, une explication simple avec un exemple, puis 3 exercices progressifs avec leur corrigé.
```

### Pour l'élève tuteur : expliquer sans donner la réponse

```text
Mon camarade bloque sur cet exercice : [ÉNONCÉ]. Donne-moi une série de questions à lui poser pour le guider vers la solution sans lui donner la réponse. Classe-les de la plus ouverte à la plus précise.
```

### Pour l'élève aidé : formuler ma difficulté

```text
Je n'arrive pas à avancer sur [NOTION OU EXERCICE]. À partir de mes sources, pose-moi 3 questions courtes pour m'aider à identifier précisément ce que je n'ai pas compris, puis dis-moi quelle partie du cours relire en priorité.
```

### Bilan de séance

```text
Voici ce que nous avons fait pendant la séance de tutorat : [RÉSUMÉ]. Génère un bilan en 5 lignes : ce qui est acquis, ce qui reste fragile, et deux exercices à refaire seul avant la prochaine séance.
```

## 2.3 Grand oral

!!! note "Sources conseillées"

    Charge dans le carnet : le programme de ta spécialité, les articles, vidéos ou ouvrages sur lesquels tu t'appuies, et tes notes personnelles. Plus les sources sont précises, plus les questions seront pertinentes.

### Trouver des idées de sujets

```text
D'après le programme de [SPÉCIALITÉ 1] et de [SPÉCIALITÉ 2] dans ces sources, propose 10 questions possibles pour le Grand oral. Chaque question doit : relier les deux spécialités ou approfondir l'une d'elles, être formulée comme une vraie problématique, et être traitable en 5 minutes. Indique pour chacune la notion du programme concernée.
```

### Évaluer une idée de sujet

```text
Voici ma question de Grand oral : « [QUESTION] ». D'après mes sources, est-elle assez précise et traitable en 5 minutes ? Quels sont les points forts de cette question, ses risques (trop vaste, hors programme, trop technique) et comment la reformuler pour l'améliorer ?
```

### Construire un plan

```text
À partir de mes sources, propose un plan en trois parties pour répondre à la question « [QUESTION] ». Pour chaque partie : l'idée principale, un exemple ou une démonstration à présenter, et la source sur laquelle m'appuyer. Prévois une introduction qui pose la problématique et une conclusion qui ouvre sur autre chose.
```

### Questions du jury

```text
Joue le rôle d'un jury de Grand oral. À partir de mes sources et de mon sujet « [QUESTION] », pose-moi 10 questions possibles pour la partie d'échange, de la plus simple à la plus difficile. Précise pour chacune si elle porte sur mon sujet, sur le programme ou sur mon projet d'orientation.
```

### Entraînement interactif

```text
Fais-moi passer un entraînement d'échange avec le jury sur mon sujet « [QUESTION] ». Pose-moi une question à la fois, attends ma réponse, puis dis-moi si elle est précise, si elle est cohérente avec mes sources et comment la rendre plus convaincante. Pose ensuite une question de relance.
```

### Vulgariser un point technique

```text
Voici une notion technique de mon sujet : [NOTION]. D'après mes sources, aide-moi à l'expliquer en 1 minute à quelqu'un qui n'a pas fait la spécialité, avec une image ou un exemple de la vie courante. Signale les approximations à éviter.
```

### Lien avec mon projet d'orientation

```text
À partir de mes sources, aide-moi à relier mon sujet « [QUESTION] » à mon projet d'orientation vers [FORMATION OU MÉTIER]. Propose 3 façons de présenter ce lien en 1 minute, sans que cela paraisse artificiel.
```

## 2.4 Projet NSI

### Cahier des charges

```text
À partir de mes sources, aide-moi à rédiger le cahier des charges de mon projet [DESCRIPTION]. Il doit contenir : l'objectif, les fonctionnalités minimales et optionnelles, les notions du programme utilisées, la répartition des tâches entre les membres du groupe et un calendrier.
```

### Documentation d'un projet

```text
À partir de ce code et de ces notes, rédige une documentation pour un utilisateur : à quoi sert le programme, comment l'installer et le lancer, un exemple d'utilisation et les limites connues.
```

---

# 3. Perso

## 3.1 Notices, pannes et garanties

Charge dans un carnet « Maison » les notices en PDF, les factures, les contrats et les garanties.

### Mode d'emploi

```text
Comment faire [TÂCHE PRÉCISE] avec mon [PRODUIT] ? Donne-moi les instructions pas à pas d'après la notice, en indiquant la page ou la section.
```

### Diagnostic de panne

```text
Mon [PRODUIT] présente [SYMPTÔME]. D'après la notice et les documents de garantie, quelles sont les causes les plus probables et les solutions recommandées ? Classe-les de la plus simple à vérifier à la plus complexe, et dis-moi dans quel cas il faut contacter le service après-vente.
```

### Détails de la garantie

```text
Que dit ma garantie ou mon contrat à propos de [SITUATION PRÉCISE] ? Cite la section concernée et indique les conditions, les exclusions et les démarches à effectuer.
```

### Entretien régulier

```text
D'après les notices de ce carnet, établis un calendrier d'entretien pour [PRODUIT : chaudière, lave-linge, voiture…] avec la fréquence de chaque opération, ce qu'il faut acheter (références) et les signes qui montrent qu'il faut intervenir plus tôt.
```

## 3.2 Contrats et documents administratifs

### Résumé d'un contrat

```text
Résume ce contrat en 10 points maximum : durée, coût, conditions de résiliation, préavis, pénalités, obligations de chaque partie. Signale les clauses inhabituelles ou qui méritent une attention particulière, avec leur numéro d'article.
```

### Comparer deux offres

```text
Compare ces deux contrats (ou devis) sur les critères suivants : prix total, durée d'engagement, couverture, exclusions, conditions de résiliation. Présente le résultat dans un tableau et signale ce qui est difficile à comparer.
```

!!! warning "Précaution"

    Ces prompts aident à lire et à comparer, mais ne remplacent pas un conseil juridique ou financier. En cas d'enjeu important, vérifie auprès d'un professionnel.

## 3.3 Apprendre et se cultiver

### Synthèse d'un article ou d'une vidéo

```text
Résume cette source en 10 lignes, puis liste les 5 idées principales, les termes à connaître et 3 questions que je devrais me poser pour aller plus loin.
```

### Comparer plusieurs sources

```text
Compare ce que disent ces différentes sources sur [SUJET]. Présente-moi les points d'accord, les désaccords et ce qui n'est abordé que par une seule source. Cite-les.
```

### Parcours d'apprentissage

```text
À partir de ces sources, propose-moi un parcours d'apprentissage en [NOMBRE] étapes pour découvrir [SUJET], en partant de mon niveau actuel : [NIVEAU]. Pour chaque étape, indique quelles sources lire ou regarder, en combien de temps, et comment vérifier que j'ai compris.
```

### Préparer un voyage

```text
À partir de ces guides, articles et réservations, prépare-moi un itinéraire de [NOMBRE] jours pour [DESTINATION]. Regroupe les lieux par quartier pour limiter les trajets, indique les horaires et réservations à anticiper, et signale les informations contradictoires entre les sources.
```

---

# Variantes des prompts qui servent à plusieurs usages

Quelques prompts fonctionnent tels quels dans plusieurs contextes. Tu n'as qu'à changer la formulation du sujet.

| Prompt de base | Usage enseignant | Usage élève | Usage perso |
|---|---|---|---|
| Détection des contradictions | Comparer deux manuels | Comparer son cours avec un manuel | Comparer deux offres ou deux avis |
| Analyse des lacunes | Cours vs programme | Mes fiches vs le cours | Mes notes vs un sujet de voyage |
| Synthèse | Veille pédagogique | Fiche de révision | Article ou vidéo |
| Extraction de preuves | Où le programme parle de… | Où mon cours définit… | Où mon contrat dit que… |

```text
En te basant uniquement sur les sources de ce carnet, identifie les points où elles divergent ou se contredisent. Pour chaque désaccord, cite les deux passages, explique la nature de la différence (définition, chiffre, méthode, opinion) et indique laquelle des deux sources semble la plus fiable, en justifiant.
```

---

# Garde-fous

- **Vérifier** : un prompt ne garantit pas l'exactitude. Relis les corrigés de maths et teste le code avant de le distribuer.
- **Sources** : la qualité de la réponse dépend de celle des sources chargées. Privilégie programmes officiels, cours de la classe, manuels de référence.
- **Élèves** : l'outil aide à réviser et à comprendre, il ne remplace pas la réflexion personnelle. Les prompts de correction sont écrits pour donner des indices plutôt que la solution.
- **Données** : pas de données nominatives d'élèves ni de documents confidentiels dans les carnets partagés.
