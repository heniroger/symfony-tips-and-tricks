# Symfony Tips and Tricks V5.3

## Symfony Installation and configuration
https://symfony.com/doc/current/setup.html

### Symfony Installation
```bash

# For Symfony Website
$ composer create-project symfony/website-skeleton my_projeùct_name

# For Api based  Application,  console, microservice
$ composer create-project symfony/skeleton my_project_name
```

### Configure existing project
```bash
# Download project
$ cd projects/
$ git clone ...

# Configure project
$ cd my-project/
$ composer install
```
### Display information in .env file

```
$ php bin/console about
```

### Run project

```
$ php bin/console server:start
```

## Installing Encore
https://symfony.com/doc/current/frontend/encore/installation.html

### Installing Encore in Symfony Applications
```bash

$ composer require symfony/webpack-encore-bundle
$ yarn install
```
### Creating the webpack.config.js File

```js
const Encore = require('@symfony/webpack-encore');

// Manually configure the runtime environment if not already configured yet by the "encore" command.
// It's useful when you use tools that rely on webpack.config.js file.
if (!Encore.isRuntimeEnvironmentConfigured()) {
    Encore.configureRuntimeEnvironment(process.env.NODE_ENV || 'dev');
}

Encore
    // directory where compiled assets will be stored
    .setOutputPath('public/build/')
    // public path used by the web server to access the output path
    .setPublicPath('/build')
    // only needed for CDN's or sub-directory deploy
    //.setManifestKeyPrefix('build/')

    /*
     * ENTRY CONFIG
     *
     * Add 1 entry for each "page" of your app
     * (including one that's included on every page - e.g. "app")
     *
     * Each entry will result in one JavaScript file (e.g. app.js)
     * and one CSS file (e.g. app.css) if your JavaScript imports CSS.
     */
    .addEntry('app', './assets/app.js')
    //.addEntry('page1', './assets/page1.js')
    //.addEntry('page2', './assets/page2.js')

    // When enabled, Webpack "splits" your files into smaller pieces for greater optimization.
    .splitEntryChunks()

    // will require an extra script tag for runtime.js
    // but, you probably want this, unless you're building a single-page app
    .enableSingleRuntimeChunk()

    /*
     * FEATURE CONFIG
     *
     * Enable & configure other features below. For a full
     * list of features, see:
     * https://symfony.com/doc/current/frontend.html#adding-more-features
     */
    .cleanupOutputBeforeBuild()
    .enableBuildNotifications()
    .enableSourceMaps(!Encore.isProduction())
    // enables hashed filenames (e.g. app.abc123.css)
    .enableVersioning(Encore.isProduction())

    // enables @babel/preset-env polyfills
    .configureBabelPresetEnv((config) => {
        config.useBuiltIns = 'usage';
        config.corejs = 3;
    })

    // enables Sass/SCSS support
    //.enableSassLoader()

    // uncomment if you use TypeScript
    //.enableTypeScriptLoader()

    // uncomment to get integrity="..." attributes on your script & link tags
    // requires WebpackEncoreBundle 1.4 or higher
    //.enableIntegrityHashes(Encore.isProduction())

    // uncomment if you're having problems with a jQuery plugin
    //.autoProvidejQuery()

    // uncomment if you use API Platform Admin (composer require api-admin)
    //.enableReactPreset()
    //.addEntry('admin', './assets/admin.js')
;

module.exports = Encore.getWebpackConfig();

```
### Next, open the new assets/app.js

```js
// assets/app.js
/*
 * Welcome to your app's main JavaScript file!
 *
 * We recommend including the built version of this JavaScript file
 * (and its CSS file) in your base layout (base.html.twig).
 */

// any CSS you import will output into a single css file (app.css in this case)
import './styles/app.css';

// Need jQuery? Install it with "yarn add jquery", then uncomment to import it.
// import $ from 'jquery';

console.log('Hello Webpack Encore! Edit me in assets/app.js');

```
### And the new assets/styles/app.css file:

```css
/* assets/styles/app.css */
body {
    background-color: lightgray;
}

```

## Enabling React.js

### Install react dependencies
```bash
$ yarn add react react-dom prop-types
```
### Enable react in your webpack.config.js:
```js
  // webpack.config.js
  // ...

  Encore
      // ...
+     .enableReactPreset()
  ;
```
## Configure SplitChunck
It prevent your file to become larger,if you're using multiple jquery script and need separate code. See https://symfony.com/doc/current/frontend/encore/split-chunks.html
### Add .splitEntryChunks() in  webpack.config.js
```js
  // webpack.config.js
  Encore
      // ...

      // multiple entry files, which probably import the same code
      .addEntry('app', './assets/app.js')
      .addEntry('homepage', './assets/homepage.js')
      .addEntry('blog', './assets/blog.js')
      .addEntry('store', './assets/store.js')

+     .splitEntryChunks()
```
### If you are using twig, comment few lines
```js
{#
    May now render multiple script tags:
        <script src="/build/runtime.js" defer></script>
        <script src="/build/vendors-node_modules_jquery_dist_jquery_js.js" defer></script>
        <script src="/build/homepage.js" defer></script>
#}
{{ encore_entry_script_tags('homepage') }}
```
### Controlling how Assets are Split
```js
  // webpack.config.js
  Encore
      // ...

      .splitEntryChunks()
+     .configureSplitChunks(function(splitChunks) {
+         // change the configuration
+         splitChunks.minSize = 0;
+     })
```
