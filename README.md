# Deploying vanilla files with GitHub Pages

[⬅ Version Française](./README-FR)

Why GitHub Pages? Well, quality hosting is often not free. GitHub Pages offers a decent service free of charge.
{:.alert-info}

## What does "deploy" mean in a react context?

React is an overlay for native JS. In concrete terms, it's a JS library, a set of functions that will simplify our lives. In doing so, developers will be working with a multitude of files during the development phase.

Each time this phase is completed, the code enters the production phase, i.e. ready to be put online. React will then build our site. It will reduce all our files to optimized HTML, CSS and JS.

All you have to do is retrieve these files and put them online, as in the previous workshop: [Deploy 01 - Vanilla](https://wildcodeschool.github.io/workshop-deploy-vanilla/README-FR). Right?

Of course, that would be too easy. There are bound to be a few bugs when it comes to importing images or links, for example. Yes, DevOps is a hard work.

Fortunately, let's not forget that we're in React. There's a super-simple solution to help us out: packages.

## Preparation

Create a repository on GitHub. You can leave it public or private.

The link to the deployment will be public (seems pretty logic).

### The package of the future

Without further ado, here is the name of our new best friend: [gh-pages](https://www.npmjs.com/package/gh-pages).

Install it in your project as a development dependency: `npm i gh-pages -D`.

### With Vite, no time to waste...

... but only if you know how to configure it.

Indeed, as you generate your projects from Vite in WildCodeSchool, you'll need a few configuration touches (but this way, you'll feel like extreme Hackerz in front of your friends).

You'll need to modify the `package.json` and `vite.config.js` files (those at the root of your project).

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

## The moment of truth

Now comes the hardest part!

Issue the command `npm run deploy` in the terminal and... voilà.

"gh-pages" will configure your repository and set up the public deployment url. Ain't life too easy?
