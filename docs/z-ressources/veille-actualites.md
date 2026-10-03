---
title: Prompts de veille et d'actualités
description: Prompt de synthèse quotidienne ou hebdomadaire, à utiliser avec un assistant disposant de la recherche web.
---

# Veille et actualités

Ces prompts ne sont **pas pour NotebookLM** : ils demandent des informations récentes qui ne sont dans aucune source chargée. Il faut donc un assistant (chat) avec **la recherche web activée**. Sans cela, le modèle répond de mémoire et peut inventer des événements ou des sources.

!!! warning "Avant de s'y fier"

    - Vérifie que la recherche web est bien activée, sinon la « synthèse du jour » sera fausse.
    - Clique sur quelques liens fournis : un modèle peut se tromper sur une source ou une date.
    - Pour une information importante (faille critique, décision officielle), va à la source primaire (ANSSI, CERT-FR, site de l'éditeur, Bulletin officiel).

## Synthèse quotidienne

```text
Tu es mon analyste de veille personnel : neutre, factuel, sans hype ni commentaire émotionnel.

Date du jour : [DATE]
Période couverte : les dernières 24 heures (si nous sommes lundi : depuis vendredi).
Langue : français.

Utilise la recherche web. N'invente aucun événement, chiffre ou source. Si tu ne peux pas vérifier une information, écris « non vérifié ».

Sujets, dans cet ordre :
1. Cybersécurité : incidents majeurs, vulnérabilités critiques, attaques étatiques ou hacktivistes, annonces officielles (ANSSI, CERT-FR, éditeurs).
2. Intelligence artificielle : nouveaux modèles, recherches importantes, benchmarks, applications concrètes.
3. Sciences : physique, biologie, énergie, climat, découvertes notables.
4. Logiciels libres : Linux, outils écrits en Rust, outils écrits en Go.
5. Éducation et numérique : programmes, annonces de l'Éducation nationale, NSI et mathématiques, IA à l'école.
6. International : géopolitique, économie majeure, conflits.
7. France : politique, économie, société, si pertinent.

Règles strictes :
- Uniquement les événements réellement significatifs. Pas de bruit, pas de remplissage.
- 3 items maximum par catégorie.
- Format de chaque item : titre en gras, puis 1 à 2 phrases factuelles, puis « Impact : » en une phrase si utile.
- Pour chaque item : source (nom, lien, date) et niveau de fiabilité (officielle / presse reconnue / source unique non confirmée).
- Distingue clairement les faits des analyses ou opinions.
- Si rien d'important dans une catégorie, écris : « Rien de majeur aujourd'hui. »
- Termine par une section « Points à surveiller » : risques, suites attendues, échéances.
```

## Version hebdomadaire

Plus lisible que le quotidien si tu n'as pas le temps de lire tous les jours.

```text
Tu es mon analyste de veille personnel : neutre, factuel, sans hype.

Période couverte : du [DATE DÉBUT] au [DATE FIN]. Langue : français. Utilise la recherche web et n'invente aucune source.

Pour chacun des domaines suivants, fais le bilan de la semaine : cybersécurité, IA, sciences, logiciels libres (Linux, Rust, Go), éducation et numérique, international, France.

Pour chaque domaine :
- les 3 faits les plus importants de la semaine, avec date, source et lien ;
- une tendance de fond si elle se dégage ;
- ce qui reste à surveiller la semaine suivante.

Termine par le « Top 5 de la semaine », tous domaines confondus, avec une phrase expliquant pourquoi chaque point compte.
```

## Veille ciblée cybersécurité

```text
Tu es mon analyste en cybersécurité, factuel et sans alarmisme. Utilise la recherche web.

Période : [24 heures / 7 jours]. Langue : français.

Liste les vulnérabilités critiques et les incidents significatifs récents. Pour chacun :
- identifiant (CVE si disponible) et produit concerné ;
- gravité (score CVSS si disponible) et exploitation active ou non ;
- correctif disponible ou contournement ;
- source officielle (éditeur, CERT-FR, ANSSI) avec lien.

Classe par ordre d'urgence. Si aucun élément n'est critique, dis-le.
```

## Veille pour l'enseignement

```text
Tu es mon assistant de veille pédagogique pour un enseignant de mathématiques et de NSI au lycée. Utilise la recherche web et privilégie les sources officielles (education.gouv.fr, Éduscol, Bulletin officiel, Eduscol NSI, associations disciplinaires).

Période : [PÉRIODE]. Langue : français.

Signale uniquement ce qui concerne :
- les programmes, les épreuves et le calendrier (Grand oral, épreuves de spécialité, évaluations) ;
- les ressources officielles nouvelles ou mises à jour (Éduscol, sujets, banques d'exercices) ;
- les annonces sur le numérique et l'IA à l'école (cadres d'usage, outils autorisés) ;
- les évolutions utiles pour l'enseignement de l'informatique (Python, outils, langages).

Pour chaque item : 1 à 2 phrases, source avec lien et date, et « Ce que ça change pour moi » en une phrase. Si rien de nouveau, écris « Rien de nouveau ».
```

## Conseils d'utilisation

- **Automatiser** : certains assistants permettent de planifier une tâche récurrente (par exemple chaque matin). Dans ce cas, remplace `[DATE]` par une formulation du type « date du jour ».
- **Limiter** : plus la liste de sujets est longue, plus le résultat est superficiel. Pour un quotidien, 4 à 5 catégories suffisent.
- **Ajuster** : si les résultats sont trop bavards, ajoute « Maximum 300 mots au total ».
- **Sources** : tu peux imposer une liste de sources préférées, par exemple « privilégie ANSSI, CERT-FR, LWN, le Bulletin officiel ».
