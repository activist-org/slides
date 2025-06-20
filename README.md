<div align="center">
  <a href="https://github.com/activist-org/slides"><img src="https://raw.githubusercontent.com/activist-org/slides/main/.github/resources/SlidesGitHubBanner.png" width=1024 alt="Slides logo"></a>
</div>

[![issues](https://img.shields.io/github/issues/activist-org/slides?label=%20&logo=github)](https://github.com/activist-org/slides/issues)
[![license](https://img.shields.io/github/license/activist-org/slides.svg?label=%20)](LICENSE.txt)
[![coc](https://img.shields.io/badge/Contributor%20Covenant-ff69b4.svg)](.github/CODE_OF_CONDUCT.md)

### Presentations related to activist projects

This repo contains various presentations for activist community projects. The slides are created using [Slidev](https://github.com/slidevjs/slidev).

Suggestions for how to improve the content of these slides are more than welcome! ✨ Edits will mainly be made in the corresponding `slides.md` file for each presentation. Please see the [contributing guide](CONTRIBUTING.md) if you'd like to help.

## **Contents**

- [Developer Tools](https://github.com/activist-org/slides/tree/main/developer_tools)
  - The tools that the activist community has written to support development

## Building Slides

First clone this repository or your fork:

```bash
git clone https://github.com/activist-org/slides.git
# git clone https://github.com/<your-username>/slides.git
```

Navigate to the project and install the dependencies for all presentations:

```bash
cd slides

# Based on your package manager:
yarn install
npm install
pnpm install
```

Build and open your slides of choice by navigating to its directory and executing the `run dev` command for your package manager:

```bash
cd SLIDES_OF_CHOICE

# Based on your package manager:
yarn run dev
npm run dev
pnpm run dev
```

Once finished you can visit <http://localhost:3000> to view the slides. Follow the prompts in your terminal to close them or do other actions.
