# Notes pour le cours de Nano-ordinateurs fait par Sébastien Trottier A2024
# Transféré en A2025 à Simon Tousignant

Les notes de cours sont affichées sous la forme d'un site web de documentation grâce à [mkdocs](https://www.mkdocs.org/).

## Utilisation

- Le répertoire **docs** contient tous les fichiers de documentation.
- Chaques pages du site est un fichier de type markdown.
- Le fichier mkdocs.yml sert à définir entre autre le menu de navigation sous la section **nav:**
- Le répertoire **site** contient le build du site prêt à l'exportation.

Pour lancer le rendu du site en local 

`mkdocs serve`

Pour "builder" le site afin qu'il soit exportable

`mkdocs build`

Le site sera disponible dans le répertoire **site**. Ce répertoire est déjà relié à un autre dépôt Github Pages (https://github.com/nano-ordinateurs/nano-ordinateurs.github.io/).

## Modification du site

Quand un modification est fait dans les fichiers, faites un commit et un push. Si vous voulez mettre le site en ligne, faites un commit et un push du dépôt du répertoire **site**

## Notes

- Documentation pour le formatage : [https://squidfunk.github.io/mkdocs-material/reference/grids/](https://squidfunk.github.io/mkdocs-material/reference/grids/)
- Plugins supplémentaire utilisé : [https://www.neoteroi.dev/mkdocs-plugins/](https://www.neoteroi.dev/mkdocs-plugins/)
