---
title: Ajouter katex à mkdocs
description: Comment ajouter katex à mkdocs
---

# Ajouter Katex à MkDocs

## Le code

=== "docs/javascripts/katex.js"

    ```js title="docs/javascripts/katex.js"
    --8<-- "docs/javascripts/katex.js"
    ```

=== "mkdocs.yml"

    ```yaml title="mkdocs.yml"
    extra_javascript:
        - javascripts/katex.js
        - https://cdn.jsdelivr.net/npm/katex@0.16.3/dist/katex.min.js

    extra_css:
        - stylesheets/extra.css
        - https://cdn.jsdelivr.net/npm/katex@0.16.3/dist/katex.min.css
    ```

## Usage et personnalisation

!!!tip "Ajout de macros"

    On peut parfaitement ajouter des **macros** personnalisées, comme avec `#!latex \newcommand`

    === "katex.js"

        ```js title="docs/javascripts/katex.js" hl_lines="3 4 5 6"
        (function () {
            'use strict';
            const macros = {
                "\\RR": "\\mathbb{R}",
                "\\vect": "{\\begin{pmatrix}#1\\\\#2\\end{pmatrix}}"
            };
        ...
        ```

    === "Markdown"

        ```latex
        Vectors in $\RR^2$ have a shape of

        $$\vect{x}{y}$$
        ```

    === "Rendu"

        Vectors in $\RR^2$ have a shape of

        $$\vect{x}{y}$$
