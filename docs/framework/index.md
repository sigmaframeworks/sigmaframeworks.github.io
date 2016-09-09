---
title: Getting Started
layout: docs-layout
---

# Getting Started

--------------------------------------------------------------------------------

## Start with Skeleton Project

Starting a project with `aurelia-cli` and `ui-skeleton` project.

- ###### Download the skeleton project [here](//github.com/sigmaframeworks/sigma-ui-skeleton/archive/framework.zip)

- ###### Setup npm pre-requisites

  - Install `node`
  - Install `aurelia-cli`

    ```bash
    npm -g install aurelia-cli
    ```

- ###### Create an aurelia project

  ```bash
  mkdir <project_dir>
  cd <project_dir>
  au new --here

  npm install sigma-ui-framework --save
  ```

- ###### Replace generated files with skeleton files

  ```bash
  cp -r <skeleton_dir>/* .
  ```

- ###### Update `<project_dir>/aurelia_project/aurelia.json`

  - Change `"stub": true` to `"stub": false`

  - Add to `transpiler/dtsSource`<br>

    ```
    "./node_modules/sigma-ui-libs/typings/*.d.ts",
    "./node_modules/sigma-ui-framework/dist/typings/**/*.d.ts"
    ```

  - Add to `bundles` object after `app-bundle.js`

    ```json
    {
        "name": "ui-framework.js",
        "prepend": [
          "node_modules/whatwg-fetch/fetch.js",
          // add if using amCharts
          "node_modules/fabric/dist/fabric.js",
          "node_modules/amcharts/dist/amcharts/amcharts.js",
          "node_modules/amcharts/dist/amcharts/pie.js",
          "node_modules/amcharts/dist/amcharts/serial.js",
          "node_modules/amcharts/dist/amcharts/themes/light.js",
          "node_modules/amcharts/dist/amcharts/plugins/export/export.js"
          // ------------
        ],
        "dependencies": [
          "lodash",
          "moment",
          "numeral",
          "aurelia-fetch-client",
          {
            "name": "text",
            "path": "../scripts/text"
          },
          {
            "name": "kramed",
            "path": "../node_modules/kramed/lib",
            "main": "kramed"
          },
          {
            "name": "aurelia-validation",
            "path": "../node_modules/aurelia-validation/dist/amd",
            "main": "aurelia-validation"
          },
          // add if using datagrid with large data
          {
            "name": "aurelia-ui-virtualization",
            "path": "../node_modules/aurelia-ui-virtualization/dist/amd",
            "main": "aurelia-ui-virtualization"
          },
          // ------------
          // add if using `aurelia-i18n` plugin
          {
            "name": "i18next",
            "path": "../node_modules/i18next/dist/umd",
            "main": "i18next"
          },
          {
            "name": "i18next-xhr-backend",
            "path": "../node_modules/i18next-xhr-backend/dist/umd",
            "main": "i18nextXHRBackend"
          },
          {
            "name": "aurelia-i18n",
            "path": "../node_modules/aurelia-i18n/dist/amd",
            "main": "aurelia-i18n"
          },
          // ------------
          {
            "name": "sigma-libs",
            "path": "../node_modules/sigma-libs",
            "main": "index"
          }, {
            "name": "sigma-ui-framework",
            "path": "../node_modules/sigma-ui-framework",
            "main": "sigma-ui-framework"
          }
        ]
    }
    ```

- ###### Development and Deployment

  - `au run --watch`: Run project in development mode, serves the built project on `localhost:9000`
  - `au build --env prod`: Build project for production deployment
  - `gulp prod`: Build sass files and copy required files to deployment ready folder `dist/`

--------------------------------------------------------------------------------

## Aurelia Entry Point

- `src/main.ts` Main aurelia entry point

  ```typescript
  aurelia.use
    .plugin('aurelia-validation')
    // Add the following to use aurelia-i18n internalization plugin
    .plugin('aurelia-i18n', (instance) => {
            instance.i18next.use(Backend);
            return instance.setup({
                backend: { loadPath: './locales/{{lng}}/{{ns}}.json' },
                lng: 'de',
                attributes: ['t', 'i18n'],
                fallbackLng: 'en',
                debug: false
            });
        })
    .plugin('sigma-ui-framework', function(config) {
      config
        .title(string)
        .version(string)
        .appKey(string)

        .apiUrl(url)
        .apiHeaders(object)
        // Send authorization header with every request
        .addAuthHeader(bool)

        .useAmCharts()
        .languages(array<{id, name}>)
    });

  aurelia.start()
    .then(() => aurelia.setRoot())
    .then(() => {
      // Remove splash
      var splash = window.document.querySelector('.ui-splash');
      splash.classList.add('animate');
      setTimeout(() => {
        splash.parentElement.removeChild(splash);
      }, 1000);
    })
    .catch(e => {
      console.log(e);
    });
  ```

  - Read about the [aurelia-i18n](https://github.com/aurelia/i18n) plugin here.
