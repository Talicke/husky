# Husky

## Initialisation

### Initialiser git flow

```bash
git flow init
```

va permettre d'initialiser le dossier avec git flow en determinant le nom des branch

* master
* develop

ainsi que le prefix des branch

* feature
* bugfix
* release
* hotfix
* support

### Installation de Husky

Husky est un utilitaire pour exécuter des hooks avant et après les commits

Installe husky comme une dependance de developpement de l'application

```bash
npm install husky --save-dev
```

ajouter un ```.gitignore``` au projet et ajouter le node_modules au fichier ignorer par git

```bash
echo 'node_modules/' >> .gitignore
```

Active husky dans le projet en creant un fichier ```.husky``` à la racine du projet

```bash
npx husky install
```

Ajoute au fichier les lignes si dessous au ```package.json``` pour permettre lors de l'installation des dépendances du projet d'activer husky

```json
"scripts": {
  "prepare": "husky install"
},
```

### Installer Commitlint

Commitlint vérifie que les commits correspondent au convention de nomage

Installer Commitlint comme une dépendance de developpement de l'application

```bash
npm install husky @commitlint/config-conventional @commitlint/cli --save-dev
```

Crée un fichier de configuration ```commitlint.config.js``` à la racine du projet et y ajouter ces lignes pour configurer commitlint sur les convention d'Angular

```js
module.exports = { extends: ['@commitlint/config-conventional'] };
```

Ajouter le hook pre-commit

```bash
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```

malheuresement cette commande ne fonctionne pas toujours,
aller dans le fichier ```.husky/_/commit-msg``` vérifier qu'il ressemble a ceci

```bash
#!/bin/sh
. "$(dirname "$0")/husky.sh"

npx --no -- commitlint --edit "$1"
```

sinon remplacer le contenu par ci-dessus

Maintenant impossible de commit sans respecter la convention Angular

### BONUS: ajouter Commitizen

Commitizen permet d'avoir une interface pour créer les commit avec la convention Angular

installer commitizen comme une dépendance de developpement de l'application

```bash
npm install commitizen --save-dev
```

activer commitizen avec la convention de nommage

```bash
npx commitizen init cz-conventional-changelog --save-dev --save-exact
```

Ajoute au fichier les lignes si dessous au ```package.json``` pour permettre de configurer Commitizen comme script NPM

```json
"scripts": {
  "commit": "cz"
}
```

note : attention si vous avez suivie toutes les etapes la partie script du fichier ```package.json``` resemble à ça

```json
"scripts": {
    "prepare": "husky install",
    "commit": "cz"
  },
```

maintenant pour lancer une commit avec commitizen

```bash
npm run commit
```
