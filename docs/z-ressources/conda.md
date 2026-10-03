---
title: Python - Conda, Miniconda, Anaconda
description: Utilisation de conda, miniconda ou anaconda
---

Documentation de référence: [https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#)

## Prérequis

On suppose ici que Anaconda ou Miniconda est installé.

- [Anaconda](https://www.anaconda.com/products/distribution)
- [Miniconda](https://docs.conda.io/en/latest/miniconda.html)

## Lister tous les environnments disponibles

```bash
conda env list
```

## Créer un nouvel environnement

```bash
conda create --name envname
```

Puis pour l'activer:

```bash
conda activate envname
```

## Créer un nouvel environnement dans un dossier

```bash
conda create --prefix ./envname
```

Puis pour l'activer:

```bash
conda activate ./envname
```

## Supprimer un environnement et ses dépendances

```bash
conda remove --name envname --all
```

## Cloner un environnement existant

```bash
conda create --name clone_envname --clone envname
```

## Exporter un environnement

Créer un fichier `environment.yml`avec conda:

```bash
conda env export > environment.yml
```

## Importer un environnement

```bash
conda env create -f environment.yml
```

Avec ses propres packages:

```bash
conda env create -n [name of the environment] [python version] [packages]
```

!!!example "Exemple:"

    ```bash
    conda create --prefix ./envs jupyterlab=3.2 matplotlib=3.5 numpy=1.21
    ```

Avec un fichier

```bash
conda env create -n [name of the environment] -f [file]
```
