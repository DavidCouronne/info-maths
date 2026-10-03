---
description: Python dans ses versions 3.6 et supérieures supporte des annotations de type (ou type hints) optionnelles. Voici un tutoriel rapide sur les annotations de type Python
---

# Introduction aux Types Python

Python dans ses versions 3.6 et supérieures supporte des annotations de type (ou _type hints_) optionnelles.

Ces annotations de type constituent une syntaxe spéciale qui permet de déclarer le type d'une variable.

En déclarant les types de vos variables, cela permet aux différents outils comme les éditeurs de texte d'offrir un meilleur support.

Ce chapitre n'est qu'un **tutoriel rapide / rappel** sur les annotations de type Python.

!!! info

    Ces notations ne sont pas spécifiquement au programme de spécialité NSI, mais elles sont très pratiques !

## Motivations

Prenons un exemple simple :

```Python
def get_full_name(first_name, last_name):
    full_name = first_name.title() + " " + last_name.title()
    return full_name


print(get_full_name("john", "doe"))
```

Exécuter ce programe affiche :

```
John Doe
```

La fonction :

- Prend un `first_name` et un `last_name`.
- Convertit la première lettre de chaque paramètre en majuscules grâce à `title()`.
- Concatène les résultats avec un espace entre les deux.

```Python hl_lines="2"
def get_full_name(first_name, last_name):
    full_name = first_name.title() + " " + last_name.title()
    return full_name


print(get_full_name("john", "doe"))
```

### Limitations

C'est un programme très simple.

Mais maintenant imaginez que vous l'écriviez de zéro.

À un certain point vous auriez commencé la définition de la fonction, vous aviez les paramètres prêts.

Mais vous aviez besoin de "cette méthode qui convertit la première lettre en majuscule".

Était-ce `upper` ? `uppercase` ? `first_uppercase` ? `capitalize` ?

Vous essayez donc d'utiliser le vieil ami du programmeur, l'auto-complétion de l'éditeur.

Vous écrivez le premier paramètre, `first_name`, puis un point (`.`) et appuyez sur `Ctrl+Espace` pour déclencher l'auto-complétion.

Mais malheureusement, rien d'utile n'en résulte :

<img src="https://fastapi.tiangolo.com/img/python-types/image01.png">

### Ajouter des types

Modifions une seule ligne de la version précédente.

Nous allons changer seulement cet extrait, les paramètres de la fonction, de :

```Python
    first_name, last_name
```

à :

```Python
    first_name: str, last_name: str
```

C'est tout.

Ce sont des annotations de types :

```Python hl_lines="1"
def get_full_name(first_name: str, last_name: str):
    full_name = first_name.title() + " " + last_name.title()
    return full_name


print(get_full_name("john", "doe"))
```

À ne pas confondre avec la déclaration de valeurs par défaut comme ici :

```Python
    first_name="john", last_name="doe"
```

C'est une chose différente.

On utilise un deux-points (`:`), et pas un égal (`=`).

Et ajouter des annotations de types ne crée normalement pas de différence avec le comportement qui aurait eu lieu si elles n'étaient pas là.

Maintenant, imaginez que vous êtes en train de créer cette fonction, mais avec des annotations de type cette fois.

Au même moment que durant l'exemple précédent, vous essayez de déclencher l'auto-complétion et vous voyez :

<img src="https://fastapi.tiangolo.com/img/python-types/image02.png">

Vous pouvez donc dérouler les options jusqu'à trouver la méthode à laquelle vous pensiez.

<img src="https://fastapi.tiangolo.com/img/python-types/image03.png">

## Plus de motivations

Cette fonction possède déjà des annotations de type :

```Python hl_lines="1"
def get_name_with_age(name: str, age: int):
    name_with_age = name + " is this old: " + age
    return name_with_age
```

Comme l'éditeur connaît le type des variables, vous n'avez pas seulement l'auto-complétion, mais aussi de la détection d'erreurs :

<img src="https://fastapi.tiangolo.com/img/python-types/image04.png">

Maintenant que vous avez connaissance du problème, convertissez `age` en <abbr title="string">chaine de caractères</abbr> grâce à `str(age)` :

```Python hl_lines="2"
def get_name_with_age(name: str, age: int):
    name_with_age = name + " is this old: " + str(age)
    return name_with_age
```

## Déclarer des types

Vous venez de voir là où les types sont généralement déclarés : dans les paramètres de fonctions.

### Types simples

Vous pouvez déclarer tous les types de Python, pas seulement `str`.

Comme par exemple :

- `int`
- `float`
- `bool`
- `bytes`

```Python hl_lines="1"
def get_items(item_a: str, item_b: int, item_c: float, item_d: bool, item_e: bytes):
    return item_a, item_b, item_c, item_d, item_d, item_e

```

### Types génériques avec des paramètres de types

Il existe certaines structures de données qui contiennent d'autres valeurs, comme `dict`, `list`, `set` et `tuple`. Et les valeurs internes peuvent elles aussi avoir leurs propres types.

Pour déclarer ces types et les types internes, on utilise le module standard de Python `typing`.

Il existe spécialement pour supporter ces annotations de types.

#### `List`

Par exemple, définissons une variable comme `list` de `str`.

Importez `List` (avec un `L` majuscule) depuis `typing`.

```Python hl_lines="1"
from typing import List


def process_items(items: List[str]):
    for item in items:
        print(item)
```

Déclarez la variable, en utilisant la syntaxe des deux-points (`:`).

Et comme type, mettez `List`.

Les listes étant un type contenant des types internes, mettez ces derniers entre crochets (`[`, `]`) :

```Python hl_lines="4"
from typing import List


def process_items(items: List[str]):
    for item in items:
        print(item)
```

!!! tip "Astuce"

    Ces types internes entre crochets sont appelés des "paramètres de type".

    Ici, `str` est un paramètre de type passé à `List`.

Ce qui signifie : "la variable `items` est une `list`, et chacun de ses éléments a pour type `str`.

En faisant cela, votre éditeur pourra vous aider, même pendant que vous traitez des éléments de la liste.

<img src="https://fastapi.tiangolo.com/img/python-types/image05.png">

Sans types, c'est presque impossible à réaliser.

Vous remarquerez que la variable `item` n'est qu'un des éléments de la list `items`.

Et pourtant, l'éditeur sait qu'elle est de type `str` et pourra donc vous aider à l'utiliser.

#### `Tuple` et `Set`

C'est le même fonctionnement pour déclarer un `tuple` ou un `set` :

```Python hl_lines="1  4"
from typing import Set, Tuple


def process_items(items_t: Tuple[int, int, str], items_s: Set[bytes]):
    return items_t, items_s
```

Dans cet exemple :

- La variable `items_t` est un `tuple` avec 3 éléments, un `int`, un deuxième `int`, et un `str`.
- La variable `items_s` est un `set`, et chacun de ses éléments est de type `bytes`.

#### `Dict`

Pour définir un `dict`, il faut lui passer 2 paramètres, séparés par une virgule (`,`).

Le premier paramètre de type est pour les clés et le second pour les valeurs du dictionnaire (`dict`).

```Python hl_lines="1  4"
from typing import Dict


def process_items(prices: Dict[str, float]):
    for item_name, item_price in prices.items():
        print(item_name)
        print(item_price)
```

Dans cet exemple :

- La variable `prices` est de type `dict` :
  - Les clés de ce dictionnaire sont de type `str`.
  - Les valeurs de ce dictionnaire sont de type `float`.

#### `Optional`

Vous pouvez aussi utiliser `Optional` pour déclarer qu'une variable a un type, comme `str` mais qu'il est "optionnel" signifiant qu'il pourrait aussi être `None`.

```Python hl_lines="1  4"
from typing import Optional


def say_hi(name: Optional[str] = None):
    if name is not None:
        print(f"Hey {name}!")
    else:
        print("Hello World")
```

Utiliser `Optional[str]` plutôt que `str` permettra à l'éditeur de vous aider à détecter les erreurs où vous supposeriez qu'une valeur est toujours de type `str`, alors qu'elle pourrait aussi être `None`.

#### Types génériques

Les types qui peuvent contenir des paramètres de types entre crochets, comme :

- `List`
- `Tuple`
- `Set`
- `Dict`
- `Optional`
- ...et d'autres.

sont appelés des **types génériques** ou **Generics**.

### Classes en tant que types

Vous pouvez aussi déclarer une classe comme type d'une variable.

Disons que vous avez une classe `Person`, avec une variable `name` :

```Python hl_lines="1-3"
class Person:
    def __init__(self, name: str):
        self.name = name


def get_person_name(one_person: Person):
    return one_person.name
```

Vous pouvez ensuite déclarer une variable de type `Person` :

```Python hl_lines="6"
class Person:
    def __init__(self, name: str):
        self.name = name


def get_person_name(one_person: Person):
    return one_person.name
```

Et vous aurez accès, encore une fois, au support complet offert par l'éditeur :

<img src="https://fastapi.tiangolo.com/img/python-types/image06.png">
