# Déployer un projet React avec GitHub Pages

[⬅ English version](./)

Pourquoi GitHub Pages ? Et bien les hébergements de qualité sont souvent payants. GitHub Pages propose un service correct gratuitement.
{:.alert-info}

## Que veut dire "déployer en React" ?

React est une surcouche au JS natif. Concrètement, c'est une bibliothèque JS, donc un ensemble de fonctions, qui vont nous simplifier la vie. Ce faisant, les développeurs vont travailler avec une multitude de fichiers pendant la phase de développement.

À chaque fois que cette phase est achevée, le code passe en phase de production, c'est-à-dire prêt à être mis sur internet. React va alors construire (on parle de "build") notre site. Il va réduire tous nos fichiers à un fichier HTML, un CSS et un JS optimisés.

Ainsi, il suffirait de récupérer ces fichiers et de les mettre en ligne comme dans l'atelier précédent : [Deploy 01 - Vanilla](https://wildcodeschool.github.io/workshop-deploy-vanilla/README-FR).

Mais bien sûr, ce serait trop facile. Il risque d'y avoir quelques bogues au niveau des imports d'images ou de liens par exemple. Hé oui, DevOps, c'est un métier.

Heureusement, n'oublions pas qu'on est en React. Il existe une solution super simple pour nous aider : les packages.

## Préparation

Créer un dépôt sur GitHub. Vous pouvez le laisser public ou privé.

Le lien pour accéder au déploiement, lui, sera public (en même temps, à quoi ça servirait sinon ?).

### Le package du futur

Sans plus attendre, voici le nom de notre nouveau meilleur ami : [gh-pages](https://www.npmjs.com/package/gh-pages).

Installez le dans votre projet en tant que dépendance de développement : `npm i gh-pages -D`.

### Avec Vite, tout va plus vite...

... mais à condition de savoir le configurer.

En effet, comme à la Wild vous générez vos projets à partir de Vite, il faut quelques touches de configuration (mais comme ça, vous aurez l'impression d'être des Hackerz de l'extrême devant vos amis).

Il va vous falloir modifier les fichiers `package.json` et `vite.config.js` (ceux à la racine de votre projet).

#### package.json

```diff
{
  "name": "{nom_de_votre_projet}",
  "private": true,
  "version": "0.0.0",
  "type": "module",
+ "homepage": "https://{votre_nom_d'utilisateur}.github.io/{nom_de_votre_dépôt}/",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
+   "predeploy" : "npm run build",
+   "deploy" : "gh-pages -d dist",
  },
// la suite //
}
```

#### vite.config.js

```diff
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
+ base: "/{nom_de_votre_dépôt}/"
})
```

## Le moment de vérité

Maintenant, le plus dur reste à faire !

Il faut lancer la commande `npm run deploy` dans le terminal et... voilà.

"gh-pages" va configurer tout seul votre dépôt et mettre en place l'url de déploiement public. Elle est pas belle la vie ?
