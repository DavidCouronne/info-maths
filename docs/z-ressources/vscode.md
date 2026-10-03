---
tile: Visual Studio Code avec Python, LaTex et Markdown
description: Comment bien utiliser Visual Studio Code pour travailler avec Python, LaTeX et Markdwon. Avec en bonus un peu de HTML, CSS et ... Javascript !!!
---

# Visual Studio Code

!!!savoir "A retenir"

        Visual Studio Code, c'est le couteau suisse du programmeur !

## Téléchargement

[https://code.visualstudio.com/](https://code.visualstudio.com/)

???info "En ligne de commande"

    === "Windows"

        Si vous êtes sous Windows 11 ou une version récente de Windows 10, vous avez les [winget tools](https://learn.microsoft.com/en-us/windows/package-manager/winget/) d'installés

        ```bash
        winget install Microsoft.VisualStudioCode --override '/SILENT /mergetasks="!runcode,addcontextmenufiles,addcontextmenufolders"'
        ```

    === "macOs"

        ```bash
        brew install --cask visual-studio-code
        ```

## Extensions utiles

1.  Material Icon Theme
2.  Latex Workshop:

    - proposée à l'installation si vous ouvrez un fichier `.tex`
    - voir plus bas pour la configuration.

## Utiliser le formateur Python Black avec Visual Studio Code

[Black](https://pypi.org/project/black/) est "le formateur de code Python sans compromis".

Il peut être configuré pour formater automatiquement votre code chaque fois que vous enregistrez un fichier
dans VSCode.

Installez Black dans votre environnement:

=== "conda"

    ```bash
    conda install -c conda-forge black jupyter-black
    ```

=== "pip"

    ```bash
    pip install black jupyter-black
    ```

=== "poetry"

    ```bash
    poetry add black jupyter-black -D
    ```

2. Dans les préférences de VS Code, recherchez "python formatting provider" puis sélectionnez "black".

3. Cherchez ensuite "format on save" et cochez la case "Editor: Format on Save"

!!!example "Exemple"

    === "Avant formattage"

        ```python
        a=2
        a=5+3
        ```

    === "Après formattage"

        ```python
        a = 2
        a = 5 + 3
        ```

## Faire du Latex avec Visual Studio Code

### Préparation de l'environnement de travail

=== "macOs"

    Sur Mac:

    ```bash
    sudo cpan -i YAML::Tiny File::HomeDir Unicode::GCString
    ```

    [https://tex.stackexchange.com/questions/390433/how-can-i-install-latexindent-on-macos](https://tex.stackexchange.com/questions/390433/how-can-i-install-latexindent-on-macos)

=== "Windows"

    Si vous êtes sous Windows 11 ou une version récente de Windows 10, vous avez les [winget tools](https://learn.microsoft.com/en-us/windows/package-manager/winget/) d'installés

    1. Il faut avoir [Perl](https://strawberryperl.com/) d'installé.

    ```bash
    winget install --id StrawberryPerl.StrawberryPerl -e --source winget
    ```

    2. Régler les variables d'environnement:

        1. Presser Windows+R puis taper le texte `sysdm.cpl`
        2. Aller à l'onglet "Paramètres systèmes avancés" puis "Variables d'environnement"
        3. Dans "Variables d'environnement pour ...", cliquez sur "Nouvelles..."
        4. "Nom de la variable": `Perl` et "Valeur de la variable": `C:\Strawberry\perl\bin`
        5. Testez en tapant `cpan -v`. Si vous avez un message d'erreur du type "cpan : Le terme «cpan» n'est pas reconnu comme nom d'applet de commande,", vous devrez peut-être redémarrer l'ordinateur.

    3. Ensuite:

        ```bash
        miktex packages install latexmk latexindent
        ```

        Ou bien, si vous avez une installation en administreur:

        ```bash
        miktex --admin packages install latexmk latexindent
        ```
    4. Pour terminer:

        ```bash
        cpan -i YAML::Tiny File::HomeDir Unicode::GCString
        ```

### Installer et configurer LaTeX Workshop

Il suffit d'ouvrir un fichier ".tex" pour que VS Code propose d'installer l'extension LaTeX Workshop

#### Pour compiler en xelatex ou en lualatex:

Dans les préférences, rechercher `latex-workshop.latex.tools`

Puis modifier à votre convenance, par exemple:

```json hl_lines="7"
"latex-workshop.latex.tools": [

    {
      "name": "latexmk",
      "command": "latexmk",
      "args": [
        "-lualatex",
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "-outdir=%OUTDIR%",
        "%DOC%"
      ],
```

#### Pour ajouter des extension pour "cleaner" les fichiers auxiliiares

Rechercher `latex-workshop.latex.clean.fileTypes`

Puis ajouter ce que vous voulez, par exemple `*.cor`

## Installer Git

=== "Windows"

    Si vous êtes sous Windows 11 ou une version récente de Windows 10, vous avez les [winget tools](https://learn.microsoft.com/en-us/windows/package-manager/winget/) d'installés

    ```bash
    winget install --id Git.Git -e --source winget
    ```

=== "macOs"

    Apple fournit un packet de Git avec [Xcode](https://developer.apple.com/xcode/).
