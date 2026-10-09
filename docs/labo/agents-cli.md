---
title: Agents et CLI en Python
description: Idées d'agents et de CLI pour l'enseignement et l'usage familial, prompts associés et agent de rédaction Markdown.
---

# Agents et CLI en Python

Cette page regroupe des idées d'agents à exécuter en ligne de commande sur un Mac, pour l'enseignement des mathématiques et de la NSI et pour un usage personnel. Elle contient aussi le prompt d'un agent de rédaction de fichiers Markdown pour un site Zensical.

Les prompts de plus de 15 lignes sont placés dans des blocs repliables. Pour les copier, déplier le bloc puis utiliser le bouton de copie.

## Principes de conception

- Faire repérer l'information par le modèle et faire exécuter les modifications par le programme.
- Ne jamais écraser l'original : écrire dans un dossier de sortie séparé ou versionner avec Git.
- Prévoir un contrôle déterministe à chaque étape : compilation LaTeX, comparaison avant/après, validation d'un schéma JSON, cohérence du nombre d'éléments.
- Demander une validation humaine avant toute action irréversible (renommer, supprimer, envoyer un message).
- Utiliser des sorties structurées (JSON) plutôt que du texte libre.
- Tenir un journal : fichier traité, réponse reçue, coût estimé.
- Regrouper les fonctionnalités dans un seul outil à sous-commandes autour d'un même catalogue de fichiers.
- Commencer par une sous-commande testée sur une dizaine de fichiers, comparés à la main, avant d'automatiser.

!!! warning "Données personnelles"

    Anonymiser tout contenu concernant des élèves avant l'envoi à une API. Pour les documents familiaux (impôts, santé, banque), envisager un modèle local plutôt qu'une API distante.

## Découper des sujets LaTeX

### Prompt actuel (AI Studio)

Ce prompt fonctionne sur les quatre fichiers testés. Il demande au modèle de réécrire l'intégralité du sujet.

??? note "Prompt actuel : découpage en environnements exercice"

    ```text
    Tu es un agent expert en traitement de documents LaTeX pour un enseignant de mathématiques au lycée.

    Ton rôle est de recevoir le code source d'un sujet de baccalauréat (provenant de l'APMEP), d'ignorer le préambule (avant \begin{document}), et de découper le corps du texte en blocs d'exercices standardisés.

    Règles de formatage strictes :
    1. Chaque partie ou exercice doit être encapsulé dans un environnement LaTeX de la forme :
       \begin{exercice}[Thème identifié][Nombre de points]
       ... contenu de l'exercice ...
       \end{exercice}
    2. Tu dois analyser le contenu mathématique pour identifier automatiquement le **Thème** principal (ex: Suites, Probabilités, Fonctions, QCM Automatismes, etc.).
    3. Tu dois extraire le nombre de points associé (ex: [6], [5], [4]). S'il n'y a pas de barème explicite, mets [?] ou [0].
    4. Conserve l'intégralité du code LaTeX à l'intérieur de chaque exercice (tableaux, tikz, enumerate, etc.) sans altérer la syntaxe mathématique.
    5. Renvoie uniquement le code LaTeX nettoyé et découpé, prêt à être compilé.
    ```

### Limites de l'approche

- Réécrire tout le fichier expose à des omissions, des accolades modifiées ou des troncatures silencieuses sur les longs sujets.
- La réponse est plus longue et plus coûteuse que nécessaire.
- Les thèmes ne sont pas contraints : « Suites » et « Suites numériques » peuvent coexister.
- Aucune vérification automatique n'est possible tant que le texte est réécrit.

### Approche recommandée

1. Numéroter les lignes du fichier source avant l'envoi.
2. Demander au modèle uniquement des métadonnées : ligne de début, ligne de fin, thème, points, notions.
3. Insérer les environnements `exercice` par programme, sans toucher au contenu.
4. Vérifier que le texte hors balises est strictement identique à l'original.
5. Compiler le résultat et signaler les erreurs.

### Prompt avec sortie JSON

??? note "Prompt : repérage des exercices avec sortie JSON"

    ```text
    Tu es un agent d'analyse de sujets de baccalauréat de mathématiques au format LaTeX (sources APMEP). Tu ne réécris jamais le texte : tu repères les exercices.

    Entrée : le fichier source, chaque ligne précédée de son numéro (L1:, L2:, ...).

    Tâche :
    1. Ignorer tout ce qui précède \begin{document}.
    2. Repérer chaque exercice ou partie indépendante, y compris les QCM ou automatismes et les exercices à choix selon l'enseignement suivi.
    3. Pour chacun, renvoyer la ligne de début, la ligne de fin, le thème principal, les notions, le nombre de points, une difficulté de 1 à 3 et la présence d'une figure.

    Règles :
    - Thème : uniquement parmi [Suites, Fonctions, Probabilités, Géométrie dans l'espace, Combinatoire et dénombrement, QCM Automatismes, Algorithmique, Autre].
    - Points : valeur indiquée dans le texte ; si absente, null. Ne jamais inventer un barème.
    - En cas de doute sur un thème ou une borne, mettre "confiance": "faible" et expliquer en une phrase.

    Sortie : uniquement un JSON valide, sans commentaire ni balise Markdown, de la forme :
    {"sujet": {"session": "...", "annee": 0, "duree": "...", "calculatrice": null},
     "exercices": [{"numero": 1, "ligne_debut": 0, "ligne_fin": 0, "theme": "...", "notions": ["..."], "points": null, "difficulte": 1, "figure": false, "confiance": "haute", "remarque": ""}]}
    ```

### Sous-commandes possibles

| Sous-commande | Rôle |
|---|---|
| `decouper` | Repérer les exercices et produire le fichier `.tex` découpé |
| `verifier` | Comparer le texte avant et après découpage, compiler, lister les cas à confiance faible |
| `indexer` | Ajouter le sujet et ses exercices au catalogue |
| `exporter` | Produire un exercice isolé en `.tex`, en PDF ou en Markdown |

## Constituer une banque d'exercices

Prolongement naturel du découpeur : un outil unique à sous-commandes autour d'un catalogue (fichiers `.tex` et index JSON ou SQLite).

| Sous-commande | Rôle |
|---|---|
| `indexer` | Ajouter thème, notions du programme, difficulté et durée estimée à chaque exercice |
| `chercher` | Retrouver des exercices à partir d'une demande en langage naturel (« suites géométriques avec algorithmique, niveau moyen ») |
| `composer` | Assembler un devoir de durée et de total de points donnés, puis le compiler en PDF |
| `stats` | Afficher la répartition par thème, niveau et année |
| `doublons` | Repérer les exercices très proches |

Pistes complémentaires :

- Ajouter un champ « source » (session, centre, numéro) pour retrouver l'original.
- Conserver le corrigé dans un fichier associé à chaque exercice.
- Valider le catalogue par un schéma JSON.

## Corriger et vérifier

- Proposer un corrigé et un barème détaillé à partir de l'énoncé.
- Comparer une proposition de corrigé au corrigé officiel de l'APMEP et signaler les écarts.
- Relire un énoncé rédigé par l'enseignant : coquilles, ambiguïtés, enchaînement des questions.
- Recalculer les résultats numériques avec un outil de calcul formel (SymPy, par exemple) plutôt que de s'en remettre au modèle.
- Vérifier la compilation LaTeX et signaler les avertissements.

## Décliner des exercices

- Générer des variantes avec d'autres valeurs numériques et recalculer les réponses par programme.
- Produire une version avec coups de pouce pour les élèves en difficulté.
- Produire une version d'approfondissement.
- Adapter un exercice de devoir surveillé en devoir maison.
- Créer un exercice de remédiation ciblé sur une erreur fréquente.

## Convertir et publier

- Convertir un exercice LaTeX en Markdown pour le site Zensical : formules conservées, front matter (thème, niveau, source), corrigé dans un bloc repliable.
- Générer une page par exercice et une table des matières par thème.
- Produire une fiche PDF imprimable à partir d'une sélection d'exercices.
- Construire le site avec `zensical build` pour vérifier l'absence d'erreur avant publication.

## Aligner sur le programme

- Associer chaque exercice aux capacités attendues du programme officiel.
- Repérer les capacités peu représentées dans la banque (analyse des lacunes appliquée à un catalogue local).
- Comparer une progression annuelle au programme et produire un tableau des écarts.
- Suivre la couverture des thèmes sur l'année pour préparer les évaluations.

## Accompagner en NSI

- Générer des TP à trous avec corrigé et tests automatiques.
- Analyser un projet d'élèves : structure, documentation, tests, rapport de relecture. Exécuter le code des élèves uniquement dans un environnement isolé.
- Fournir un tuteur en terminal reprenant le prompt NSI Pal, avec journal de séance et bilan final.
- Produire des jeux de tests pour des exercices d'algorithmique et vérifier les solutions proposées.
- Créer des questions de type QCM à partir d'un cours.

## Organiser réunions et veille

- Transformer des notes de réunion anonymisées en compte rendu et en liste d'actions.
- Extraire les décisions et les échéances d'un ensemble de comptes rendus.
- Lancer chaque matin le prompt de veille et enregistrer le résultat dans un fichier daté, avec le planificateur du Mac.
- Tenir un journal de veille consultable par mot-clé.

## Agents personnels et familiaux

| Agent | Fonctionnement |
|---|---|
| Classement de documents | Surveiller un dossier « À classer », renommer chaque PDF selon une convention (date, type, fournisseur), le ranger et mettre à jour un index |
| Garanties et échéances | Extraire date d'achat, durée de garantie ou date de renouvellement des factures et contrats, puis produire un fichier calendrier |
| Questions sur les notices | Interroger un dossier de PDF et répondre en citant la page (équivalent local d'un carnet « Maison ») |
| Tuteur en terminal | Faire réviser un enfant avec un journal de séance |
| Menus et courses | Proposer un menu hebdomadaire et une liste de courses selon recettes, contraintes et stock |
| Voyage | Regrouper réservations et messages en un itinéraire daté |
| Courriers administratifs | Résumer un courrier, indiquer l'action attendue et proposer une réponse type |

## Rédiger des fichiers Markdown

### Rôle et sous-commandes

L'agent produit des pages Markdown conformes à une charte de rédaction, prêtes pour Zensical. On peut le réaliser sous forme de prompt seul, utilisé dans un chat, ou sous forme de CLI avec les sous-commandes suivantes.

| Sous-commande | Entrée | Sortie |
|---|---|---|
| `creer` | Sujet, notes, public visé | Nouvelle page `.md` |
| `convertir` | Fichier `.tex`, `.txt`, `.docx` ou liste de prompts | Page `.md` conforme à la charte |
| `relire` | Page existante | Page corrigée et liste des modifications |
| `verifier` | Page ou dossier | Rapport de conformité, sans appel au modèle |
| `decouper` | Page trop longue | Plusieurs pages et mise à jour de la navigation |
| `modeles` | Type de page | Squelette vide (page de prompts, fiche de cours, compte rendu) |

### Charte de rédaction

- Rédiger en français, sur un ton factuel, sans humour ni emoji.
- Employer l'infinitif dans les titres et les listes (Ajouter, Remplacer, Vérifier).
- Employer le « on » impersonnel quand un sujet grammatical est nécessaire (« on pourra… »).
- Réserver la deuxième personne aux prompts.
- Commencer chaque page par un front matter avec `title` et `description`, puis un seul titre de niveau 1.
- Ne pas sauter de niveau de titre.
- Placer chaque prompt, commande ou code dans un bloc de code avec indication du langage (`text` pour les prompts).
- Placer les blocs de plus de 15 lignes dans une admonition repliable.
- Limiter les admonitions non repliables à une par page, pour un risque réel (perte de données, donnée personnelle, résultat faux).
- Ne pas inventer de lien, de chiffre ou de fonctionnalité ; marquer « À compléter » si une information manque.

### Prompt système

??? note "Prompt : agent de rédaction Markdown pour Zensical"

    ```text
    Tu es un agent de rédaction de documentation en Markdown pour un site Zensical (compatible Material for MkDocs). Tu produis des fichiers .md prêts à être publiés.

    Entrée : un sujet, des notes ou un contenu brut (texte, LaTeX, liste de prompts), et éventuellement le public visé et le type de page.
    Sortie : uniquement le contenu du fichier Markdown, sans commentaire avant ni après, sans balise englobante.

    Structure :
    - Commencer par un front matter YAML contenant title et description.
    - Un seul titre de niveau 1, identique à title. Pas de saut de niveau entre les titres suivants.
    - Introduction de 2 à 4 phrases après le titre.
    - Terminer par une section de points de vigilance seulement si le sujet le justifie.

    Style :
    - Français, ton factuel, sans humour, sans emoji, sans formule de politesse.
    - Titres et puces à l'infinitif (Ajouter, Vérifier, Remplacer). Quand un sujet grammatical est nécessaire, utiliser le « on » impersonnel (« on pourra... »). Ne jamais utiliser « tu » ni « vous » en dehors des prompts reproduits dans la page.
    - Phrases courtes, sans remplissage ni répétition entre sections.
    - Listes à puces pour les énumérations, tableaux pour les comparaisons, prose pour les explications.
    - Gras réservé aux termes clés, avec parcimonie.

    Blocs de code et prompts :
    - Placer tout prompt, commande ou code dans un bloc de code délimité par trois accents graves, avec un langage (text pour les prompts, bash, python, etc.).
    - Les prompts s'écrivent à la deuxième personne ; la règle de l'infinitif ne s'applique pas à leur contenu.
    - Bloc de plus de 15 lignes : le placer dans une admonition repliable. Syntaxe : une ligne ??? note "Titre court", une ligne vide, puis tout le contenu indenté de 4 espaces, y compris les lignes qui délimitent le bloc de code.
    - Bloc de 15 lignes ou moins : bloc de code simple, sans admonition.

    Admonitions :
    - Limiter au strict nécessaire : au maximum une admonition non repliable par page, réservée à un avertissement qui évite une erreur grave (perte de données, donnée personnelle, résultat faux).
    - Ne pas utiliser d'admonition pour une simple remarque ou un conseil : l'écrire dans le texte.
    - Types autorisés : note et warning. Toujours un titre entre guillemets.

    Contenu :
    - Ne pas inventer de fonctionnalité, de chiffre, de lien ni de référence. Si une information manque, écrire « À compléter ».
    - Reprendre à l'identique le contenu fourni qui doit être conservé tel quel (prompts, code, formules).
    - Formules : LaTeX entre $...$ ou $$...$$.
    - Liens internes en chemins relatifs.

    Avant de répondre, vérifier : front matter présent, un seul titre de niveau 1, aucun saut de niveau, titres à l'infinitif, indentation correcte des admonitions repliables, aucun bloc de plus de 15 lignes hors admonition repliable, au plus une admonition non repliable.
    ```

### Prompts complémentaires

Conversion d'un contenu existant :

```text
Convertis le contenu ci-dessous en page Markdown pour Zensical en respectant la charte de rédaction (infinitifs, « on » impersonnel, admonitions limitées, blocs de plus de 15 lignes dans des admonitions repliables). Conserve à l'identique les prompts, le code et les formules. Ne rajoute aucune information absente du contenu source. Si une information indispensable manque, écris « À compléter ».

Type de page : [fiche de cours / page de prompts / compte rendu / documentation]
Contenu :
[COLLER LE CONTENU]
```

Relecture d'une page :

```text
Relis la page Markdown ci-dessous selon la charte de rédaction. Renvoie d'abord la liste des écarts (ligne ou titre concerné, règle non respectée, correction proposée), puis la page corrigée. Ne modifie pas le sens, les prompts, le code ni les formules.

[COLLER LA PAGE]
```

### Contrôles automatiques

La sous-commande `verifier` peut s'appuyer sur des règles déterministes, sans modèle :

- Vérifier la présence et la validité du front matter YAML.
- Vérifier l'unicité du titre de niveau 1 et l'absence de saut de niveau.
- Vérifier que les blocs de code sont correctement fermés.
- Repérer les blocs de plus de 15 lignes situés hors d'une admonition repliable.
- Vérifier l'indentation de 4 espaces à l'intérieur des admonitions.
- Compter les admonitions non repliables par page.
- Contrôler les liens internes.
- Lancer `zensical build` et relever les avertissements.

Le contrôle des verbes à l'infinitif dans les titres peut se faire par une liste de verbes ou par un appel au modèle limité aux titres.

## Ordre de développement conseillé

1. Découpeur LaTeX avec sortie JSON et vérification avant/après.
2. Indexation des exercices dans un catalogue.
3. Recherche et composition de devoirs.
4. Agent de rédaction Markdown, avec la sous-commande `verifier`.
5. Agents personnels (classement de documents, notices), selon les besoins.
