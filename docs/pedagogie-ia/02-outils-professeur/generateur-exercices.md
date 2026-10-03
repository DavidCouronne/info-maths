# Générateur d'Exercices et de TP

> **Statut :** Actif (Version 1.0)

## Objectif
Ce prompt permet de structurer l'aide d'un LLM pour concevoir rapidement des exercices de programmation en Python, des activités de manipulation de données (Pandas) ou des problèmes de mathématiques adaptés aux programmes du lycée (Première / Terminale).

---

## Le Prompt Type

```text
Agis en tant qu'expert pédagogique et enseignant de Numérique et Sciences Informatiques (NSI) et de Mathématiques en lycée. 
Je souhaite concevoir une [préciser le type de ressource : ex: activité pratique / feuille d'exercices / sujet type bac pratique] sur le thème suivant : [insérer le thème, ex: la Programmation Orientée Objet en Python / les arbres binaires / les suites numériques].

Contraintes à respecter :
1. Niveau ciblé : [Première NSI / Terminale NSI / Spécialité Maths Terminale].
2. Structure : Propose une progression pédagogique allant de l'exercice d'application directe à un problème de synthèse plus complexe.
3. Code / Exemples : Fournis des squelettes de code Python propres, documentés (docstrings), accompagnés de quelques jeux de tests (assertions ou tests unitaires basiques).
4. Correction : Rédige une correction détaillée, commentée et rigoureuse pour chaque exercice.
```