<div align="center">
  <a href="https://codeberg.org/activist-org/slides"><img src="https://codeberg.org/activist-org/slides/raw/branch/main/.github/resources/SlidesGitHubBanner.png" style="width: 100%; max-width: 100%;" alt="Slides logo"></a>
</div>

[![issues](https://img.shields.io/gitea/issues/open/activist-org/slides?gitea_url=https://codeberg.org&label=%20&logo=codeberg&logoColor=ffffff)](https://codeberg.org/activist-org/slides/issues)
[![license](https://img.shields.io/github/license/activist-org/slides.svg?label=%20)](LICENSE.txt)
[![coc](https://img.shields.io/badge/Contributor%20Covenant-ff69b4.svg)](.github/CODE_OF_CONDUCT.md)

### Presentations related to activist projects

This repo contains various presentations for activist community projects. The slides are created using [Slidev](https://github.com/slidevjs/slidev).

Suggestions for how to improve the content of these slides are more than welcome! ✨ Edits will mainly be made in the corresponding `slides.md` file for each presentation. Please see the [contributing guide](CONTRIBUTING.md) if you'd like to help.

## Contents

- [i18n-check](https://codeberg.org/activist-org/slides/src/branch/main/i18n_check)
  - Presenting the [i18n-check](https://github.com/activist-org/i18n-check) project activist uses for i18n key-value validation

## Running Slides

### Prerequisites

1. [Node.js](https://nodejs.org): latest v20+ recommended
2. [Yarn](https://yarnpkg.com/): latest v4+, which will be activated automatically via [Corepack](https://yarnpkg.com/getting-started/qa#using-corepack)

### Building Slides

First clone this repository or your fork:

```bash
git clone https://codeberg.org/activist-org/slides.git
# git clone https://codeberg.org/<your-username>/slides.git
```

Navigate to the project and install the dependencies for all presentations:

```bash
cd slides

corepack enable
yarn install

# Alternatively:
npm install
pnpm install
```

Build and open your slides of choice by navigating to its directory and executing the `run dev` command for your package manager:

```bash
cd SLIDES_OF_CHOICE
yarn run dev

# Alternatively:
npm run dev
pnpm run dev
```

Once finished you can visit <http://localhost:3000> to view the slides. Follow the prompts in your terminal to close them or do other actions.
