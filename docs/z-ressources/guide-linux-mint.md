---
title: Guide de configuration Linux Mint
description: TeX Live, VS Code, navigateurs et environnement Python (uv, conda) en ligne de commande
icon: lucide/terminal
---

# Guide de configuration Linux Mint (Cinnamon)

Ce guide suppose que **Linux Mint 22.x (Cinnamon)** est déjà installé, avec un compte disposant des droits `sudo`.
Mint 22 est basée sur **Ubuntu 24.04 (« noble »)**. Toutes les commandes sont prévues pour être copiées-collées telles quelles dans un terminal (++ctrl+alt+t++).

!!! info "Conventions"

    - Les blocs de code ne contiennent **pas** de `$` en début de ligne : vous pouvez les copier en entier.
    - Les commandes avec `sudo` demandent votre mot de passe.
    - Les fichiers créés avec `cat > ... << 'EOF'` s'écrivent d'un seul coup : copiez le bloc complet, de `cat` jusqu'au `EOF` final.

---

## 1. Préparation du système

Mise à jour initiale et outils de base utilisés dans la suite du guide :

```bash
sudo apt update && sudo apt full-upgrade -y
sudo apt install -y curl wget gpg ca-certificates apt-transport-https \
    build-essential git unzip
```

---

## 2. TeX Live (version complète)


```bash
sudo apt install -y texlive-full
```

!!! warning "Espace disque"

        `texlive-full` occupe plusieurs Go (environ 5 à 7 Go) et le téléchargement peut être long.

Vérification :

```bash
pdflatex --version
latexmk --version
```



### 2.1 Dossiers pour classes et packages personnalisés

TeX Live prévoit un répertoire utilisateur, `TEXMFHOME`, qui est parcouru **depuis n'importe quel dossier de compilation**. Vérifions son emplacement (par défaut `~/texmf`) :

```bash
kpsewhich -var-value TEXMFHOME
```

Création de l'arborescence standard :

```bash
mkdir -p ~/texmf/tex/latex/mesclasses
mkdir -p ~/texmf/tex/latex/mespackages
mkdir -p ~/texmf/bibtex/bst
mkdir -p ~/texmf/bibtex/bib
mkdir -p ~/texmf/doc/latex
```

| Dossier | Contenu |
|---|---|
| `~/texmf/tex/latex/mesclasses/` | classes `.cls` |
| `~/texmf/tex/latex/mespackages/` | packages `.sty` |
| `~/texmf/bibtex/bst/` | styles bibliographiques `.bst` |
| `~/texmf/bibtex/bib/` | bases `.bib` communes |

!!! tip "Sous-dossiers"

    TeX cherche **récursivement** dans `tex/latex/`. Vous pouvez donc ranger chaque projet dans son propre sous-dossier (`~/texmf/tex/latex/mesclasses/moncours/moncours.cls`).



!!! note "Si un fichier n'est pas trouvé"

    Actualisez l'index (rarement nécessaire pour `~/texmf`) :

    ```bash
    texhash ~/texmf
    ```


---

## 3. Visual Studio Code

Installation via le dépôt officiel Microsoft (mises à jour automatiques avec `apt`).

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /tmp/microsoft.gpg
sudo install -D -o root -g root -m 644 /tmp/microsoft.gpg /usr/share/keyrings/microsoft.gpg
rm -f /tmp/microsoft.gpg

cat << 'EOF' | sudo tee /etc/apt/sources.list.d/vscode.sources > /dev/null
Types: deb
URIs: https://packages.microsoft.com/repos/code
Suites: stable
Components: main
Architectures: amd64,arm64,armhf
Signed-By: /usr/share/keyrings/microsoft.gpg
EOF

sudo apt update && sudo apt install -y code
```



!!! note "Clé Microsoft réutilisée"

    Le fichier `/usr/share/keyrings/microsoft.gpg` sera aussi utilisé pour Edge (section suivante).

---

## 4. Navigateurs

### 4.1 Brave

Commandes officielles de Brave :

```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg \
    https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg

sudo curl -fsSLo /etc/apt/sources.list.d/brave-browser-release.sources \
    https://brave-browser-apt-release.s3.brave.com/brave-browser.sources

sudo apt update && sudo apt install -y brave-browser
```

### 4.2 Microsoft Edge

La clé Microsoft a déjà été installée à l'étape VS Code. Si vous sautez cette étape, exécutez d'abord :

```bash
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /usr/share/keyrings/microsoft.gpg > /dev/null
```

Puis :

```bash
cat << 'EOF' | sudo tee /etc/apt/sources.list.d/microsoft-edge.sources > /dev/null
Types: deb
URIs: https://packages.microsoft.com/repos/edge
Suites: stable
Components: main
Architectures: amd64
Signed-By: /usr/share/keyrings/microsoft.gpg
EOF

sudo apt update && sudo apt install -y microsoft-edge-stable
```

### 4.3 Google Chrome

Le paquet `.deb` installe lui-même le dépôt Google, donc les mises à jour passeront ensuite par `apt`.

```bash
cd /tmp
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install -y ./google-chrome-stable_current_amd64.deb
rm -f google-chrome-stable_current_amd64.deb
```

!!! warning "Avertissement « configured multiple times »"

    Si `apt update` signale qu'un dépôt (Edge, VS Code ou Chrome) est configuré en double, supprimez le fichier en trop dans `/etc/apt/sources.list.d/` (gardez un seul fichier par dépôt) :

    ```bash
    ls /etc/apt/sources.list.d/
    ```

---

## 5. Python avec uv

!!! danger "Ne touchez pas au Python du système"

    Linux Mint utilise son Python système (3.12 sur Mint 22) pour ses propres outils. Ne faites jamais `sudo pip install` ni `pip install --break-system-packages`. Avec `uv`, tout est installé dans votre dossier personnel, sans risque pour le système.

### 5.1 Installer uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Rechargez le shell puis vérifiez :

```bash
source ~/.bashrc
uv --version
```

!!! tip "Si `uv` n'est pas trouvé"

    ```bash
    source ~/.local/bin/env
    ```

    ou fermez et rouvrez le terminal.

Autocomplétion (facultatif) :

```bash
echo 'eval "$(uv generate-shell-completion bash)"' >> ~/.bashrc
echo 'eval "$(uvx --generate-shell-completion bash)"' >> ~/.bashrc
source ~/.bashrc
```

### 5.2 Gérer les versions de Python

`uv` télécharge et gère lui-même des interpréteurs Python :

```bash
uv python list
uv python install 3.13
uv python install 3.12 3.9
uv python list --only-installed
```

Pour mettre à jour les versions de Python installées par `uv` vers la dernière version corrective :

```bash
uv python upgrade
```

!!! note

    Si la commande `uv python upgrade` n'existe pas, mettez d'abord `uv` à jour (`uv self-update`).

### 5.3 Installer un outil disponible partout (`uv tool`)

Un **tool** est une application Python en ligne de commande (ruff, httpie, yt-dlp, black, etc.). Chaque outil est installé dans **son propre environnement isolé**, et son exécutable est placé dans `~/.local/bin` (déjà dans le `PATH`).

```bash
uv tool install ruff
uv tool install httpie
uv tool install yt-dlp
```

Vérifier que `~/.local/bin` est bien dans le `PATH` (à faire une fois) :

```bash
uv tool update-shell
source ~/.bashrc
```

Commandes de gestion :

```bash
uv tool list
uv tool upgrade ruff
uv tool upgrade --all
uv tool uninstall ruff
```

Exécuter un outil **sans l'installer** (environnement temporaire en cache) :

```bash
uvx ruff --version
uvx --from httpie http --version
```

Ajouter des dépendances supplémentaires à un outil :

```bash
uv tool install --with pandas --with matplotlib jupyterlab
```

Installer un outil depuis un dépôt Git :

```bash
uv tool install "git+https://github.com/utilisateur/depot.git"
```

### 5.4 Forcer la version de Python d'un outil

Certains outils anciens ne fonctionnent qu'avec une vieille version de Python (par exemple 3.9). Option `--python` :

```bash
uv python install 3.9
uv tool install --python 3.9 nom-de-loutil
```

`uv` télécharge automatiquement la version demandée si elle manque, la ligne `uv python install` est donc facultative.

Changer la version d'un outil déjà installé :

```bash
uv tool install --python 3.11 --reinstall nom-de-loutil
```

Même chose pour une exécution ponctuelle :

```bash
uvx --python 3.9 nom-de-loutil --help
```

Vérifier quelle version un outil utilise :

```bash
uv tool list --show-python
```

!!! tip "Plusieurs versions du même outil ?"

    Un outil n'a qu'une seule installation à la fois. Pour tester sur plusieurs versions de Python, utilisez `uvx --python X.Y ...`.



## 7. Tout mettre à jour

### 7.1 Commandes séparées

"Système (apt)"

    

```bash
sudo apt update && sudo apt full-upgrade -y && sudo apt autoremove -y
```

"Flatpak"

```bash
flatpak update -y
```

"uv, Python et outils"

```bash
uv self-update
uv tool upgrade --all
uv python upgrade
```



## 8. Aide-mémoire

### 8.1 Python

```bash
uv python install 3.12                          # ajouter une version de Python
uv tool install --python 3.9 outil              # outil avec une version précise
uv tool upgrade --all                           # mettre à jour tous les outils
uv add --script s.py pandas && uv run s.py      # script avec dépendances
uv init projet && cd projet && uv add pandas    # nouveau projet
```

### 8.2 LaTeX

```bash
kpsewhich -var-value TEXMFHOME                  # dossier personnel TeX
kpsewhich monstyle.sty                          # vérifier qu'un fichier est trouvé
texhash ~/texmf                                 # reconstruire l'index
```

---

## 🔗 Ressources associées

- [Configuration et extensions VS Code](vscode.md)
- [Gestion des environnements Conda](conda.md)
- [Prompts de veille et d'actualités](veille-actualites.md)

