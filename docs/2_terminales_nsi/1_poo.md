---
title: Programmation Orientée Objet
description: Programmation Orientée Objet en Python
sidebar_position: 3
---

# Programmatiion Orientée Objet

## Programme officiel

!!!tip "Contenu"

    Vocabulaire de la programmation objet :

    - classes
    - attributs
    - méthodes
    - objets

!!!tip "Capacités attendues"

    - Écrire la définition d’une classe.
    - Accéder aux attributs et méthodes d’une classe.

!!!note "Commentaire"

    On n’aborde pas ici tous les aspects de la programmation objet comme le polymorphisme et l’héritage.

## Le paradigme objet

!!!tip "Le paradigme objet en bref"

    - Un programme est un ensemble d’objets
    - La seule façon d’interagir avec un objet est d’appeler l’une de ses méthodes

!!!savoir "Objets"

    Un objet regroupe :

    - des **attributs** (contenant des valeurs)
    - des **méthodes** (des opérations/fonctions) relatives à cet objet.

    Un objet est un élément issu d'une classe. On parle aussi d'**instance** de la classe.

!!!tip "Classes"

    Les classes sont des " moules " permettant de produire des objets en
    série. On produit un objet en appelant le constructeur de la classe.

## Impératif et objet

!!!example "Impératif (Python)"

    ```python
    l=[1,2,3]
    def somme(l):
        s=0
        for e in l:
            s=s + e
        return s

    print(somme(l))
    ```

!!!example "Objet (Python)"

    ```python
    #Définition de la classe
    class listeEntier():

        def __init__(self): # (1)
            self.v = [] # (2)

        def ajouter(self, elt): # (3)
            self.v.append(elt)
        def somme(self):
            s = 0
            for e in self.valeur:
                s = s + e
            return s

    #Utilisation de la classe
    l = listeEntier() # (4)
    l.ajouter(1)     # (5)
    l.ajouter(2)
    l.ajouter(3)
    print(l.somme())
    ```

    1. Constructeur
    2. Un **attribut**
    3. Une **méthode**
    4. `l`est une **instance** de la classe `listeEntier`
    5. Appel de la méthode ajout

## Quand a-t-on besoin de la programmation objet ?

1. Quand on manipule des données de structures différentes...
2. ... mais ayant des points communs.
3. Quand des grandes familles de données se dégagent.
   Ces "familles" constitueront nos classes...

## Avantages de le programmation objet

!!!info "Encapsulation"

    **Encapsulation**: pour une meilleure structuration du code.

    Dans le code du programme, on regroupe sous un même nom (celui de la
    classe) les données et les fonctions relatives à ces données.

    L'encapsulation est un principe qui consiste à regrouper des données avec un ensemble de méthodes permettant de les lire ou de les manipuler dans le but de cacher ou de protéger certaines de ces données.

    - Les méthodes et données internes (celles plus ou moins "cachée" à l'utilisateur) sont dites **privées**.
    - Les méthodes et données accessibles à tout utilisateur (celles que les utilisateurs de la classe connaissent) sont dites **publiques**.

!!!info "Abstraction"

    **Abstraction**: pour une programmation qui s’abstrait des détails.

    Si des objets de classes différentes partagent une même méthode, on peut appeler celle-ci sans connaître, a priori, la classe/type de l’objet.

## Privé - Public

!!!tip "Privé/Public en Python"

    En Python, il y a une convention de nommage : un attribut privé est toujours préfixé (c'est-à-dire précédé) de deux espaces soulignés (tiret du bas, celui du 8).

    ```python
    self.attribut1 # Public
    self.__attribut2 # Privé
    ```

!!!info "Typage (typage dynamique en Python)"

    A l’exécution, on peut distinguer des objets produits par différentes classes.

    Exemple en Python:

    ```python
    class Point:
        def __init__(self, x, y):
            self.x = x
            self.y = y

    A = Point(2, 3)
    print(type(A)) # <class '__main__.Point'>
    ```

## Liens

http://monlyceenumerique.fr/nsi_terminale/sd/sd2_programmation_objet.php
