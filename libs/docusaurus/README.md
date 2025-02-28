# Nx Plus Docusaurus

> First class support for [Docusaurus](https://v2.docusaurus.io/) in your [Nx](https://nx.dev/) workspace.

<div align="center">
  <img src="https://raw.githubusercontent.com/ZachJW34/nx-plus/master/libs/docusaurus/nx-plus-docusaurus.png">
</div>

## Contents

- [Prerequisite](#prerequisite)
- [Getting Started](#getting-started)
- [Schematics (i.e. code generation)](#schematics-ie-code-generation)
- [Builders (i.e. task runners)](#builders-ie-task-runners)
- [Updating Nx Plus Docusaurus](#updating-nx-plus-docusaurus)
- [Troubleshooting](#troubleshooting)

## Prerequisite

If you have not already, [create an Nx workspace](https://github.com/nrwl/nx#creating-an-nx-workspace) with the following:

```
npx create-nx-workspace@^14.0.0
```

## Getting Started

### Install Plugin

```
# npm
npm install @nx-plus/docusaurus --save-dev

# yarn
yarn add @nx-plus/docusaurus --dev
```

### Generate Your App

```
nx g @nx-plus/docusaurus:app my-app
```

### Serve Your App

```
nx serve my-app
```

## Schematics (i.e. code generation)

### Application

`nx g @nx-plus/docusaurus:app <name> [options]`

| Arguments | Description           |
| --------- | --------------------- |
| `<name>`  | The name of your app. |

| Options        | Default | Description                                |
| -------------- | ------- | ------------------------------------------ |
| `--tags`       | -       | Tags to use for linting (comma-delimited). |
| `--directory`  | `apps`  | A directory where the project is placed.   |
| `--skipFormat` | `false` | Skip formatting files.                     |

## Builders (i.e. task runners)

### Dev Server

`nx serve <name> [options]`

| Arguments | Description           |
| --------- | --------------------- |
| `<name>`  | The name of your app. |

| Options     | Default     | Description                                          |
| ----------- | ----------- | ---------------------------------------------------- |
| `--port`    | `3000`      | Use specified port.                                  |
| `--host`    | `localhost` | Use specified host.                                  |
| `--hotOnly` | `false`     | Do not fallback to page refresh if hot reload fails. |
| `--open`    | `false`     | Open page in the browser.                            |

### Browser

`nx build <name> [options]`

| Arguments | Description           |
| --------- | --------------------- |
| `<name>`  | The name of your app. |

| Options            | Default | Description                                                                    |
| ------------------ | ------- | ------------------------------------------------------------------------------ |
| `--bundleAnalyzer` | `false` | Visualize size of webpack output files with an interactive zoomable treemap.   |
| `--outputPath`     | -       | The full path for the new output directory, relative to the current workspace. |
| `--minify`         | `true`  | Build website minimizing JS bundles.                                           |

## Updating Nx Plus Docusaurus

Nx Plus Docusaurus provides migrations which help you stay up to date with the latest version of Nx Plus Docusaurus.

Not only do we migrate the version of Nx Plus Docusaurus, but we also update the versions of dependencies which we install such as `@docusaurus/core` and `react`.

We recommend waiting for Nx Plus Docusaurus to update these dependencies for you as we verify that these versions work together.

### How to Migrate

#### Generate migrations.json

All you have to do to update Nx Plus Docusaurus to the latest version is run the following:

```
nx migrate @nx-plus/docusaurus
nx migrate @nx-plus/docusaurus@version # you can also specify version
```

This will fetch the specified version of `@nx-plus/docusaurus`, analyze the dependencies and fetch all the dependent packages. The process will keep going until the whole tree of dependencies is resolved. This will result in:

- `package.json` being updated
- `migrations.json` being generated

At this point, no packages have been installed, and no other files have been touched.

Now, you can inspect `package.json` to see if the changes make sense and install the packages by running `npm install` or `yarn`.

#### Run Migrations

`migrations.json` contains the transformations that must run to prepare the workspace to the newly installed versions of packages. To run all the migrations, invoke:

```
nx migrate --run-migrations=migrations.json
```

## Troubleshooting

If you encounter this error while building a Docusaurus app, then you may need to add a `terser` resolution to your `package.json`. Note: this only works with Yarn and not npm.

**Error:**

```
Docusaurus user: you probably have this known error due to using a monorepo/workspace.
We have a workaround for you, check https://github.com/facebook/docusaurus/issues/3515
```

**package.json:**

```
{
  // ...
  "resolutions": {
    "terser": "^4.0.0"
  }
  // ...
}
```

Once this has been updated, you should be able to run `yarn install` and then build your Docusaurus application.
