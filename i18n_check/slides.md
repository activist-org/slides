---
theme: default
title: i18n-check
info: |
  ## i18n-check presentation
  The project activist uses for i18n key-value validation
class: text-center mt-6
transition: slide-left
mdc: true
hideInToc: true
---

# i18n-check

<div class="pt-3">
Internationalization (i18n) key-value validation
</div>
<div class="flex flex-justify-center">
<img class="pt-6" src="/i18nCheckQRCodeWhite.png" width=136 alt="QR Code for i18n-check">
</div>

---
hideInToc: true
---

# Contents

<Toc minDepth="1" maxDepth="1" />

---

# Purpose

- The [activist.org community](https://github.com/activist-org) has a very broad need for i18n/L10n support
- Simple example localization JSON files:
  - `en.json` : `{"btn_add": "Add", "btn_remove": "Remove"}`
  - `es.json`: `{"btn_add": "Añadir", "btn_remove": "Eliminar"}`
  - `de.json`: `{"btn_add": "Hinzufügen", "btn_remove": "Entfernen"}`
- How does the development team confidently work while making sure to not break localizations?
  - We need pre-commit/[prek](https://github.com/j178/prek) based checks that are mirrored in CI
  - See our [.pre-commit-config.yaml](https://github.com/activist-org/activist/blob/main/.pre-commit-config.yaml) and [ci_i18n_check.yaml](https://github.com/activist-org/activist/blob/main/.github/workflows/ci_i18n_check.yaml)
- How can we make sure that the localization team isn't doing repeat work?
- How do we validate that localizations are being done in a consistent way across the project?

<div id="progress" class="w-1/12"/>

---

# i18n/L10n Validation CLI

## Architecture

- Written in Python using [argparse](https://docs.python.org/3/library/argparse.html) (default library)
  - Texts of files are read and parsed (no ast)
  - Robustly tested with [pytest](https://docs.pytest.org/en/stable/), validated with [ty](https://docs.astral.sh/ty/) and simplified with [complexipy](https://github.com/rohaquinlop/complexipy)
  - Fully documented in the [repo](https://github.com/activist-org/i18n-check) and on [Read the Docs](https://i18n-check.readthedocs.io/en/latest/)
- Checks are configured via an `.i18n-check.yaml` file ([view example](https://github.com/activist-org/i18n-check/blob/main/.i18n-check.yaml))
- 12 checks, with many including `--fix` options for automatic corrections

## Basics

```bash
i18n-check -gcf  # --generate-config-file
i18n-check -gtf  # --generate-test-frontends
# > Two frontends: One fails all checks and one passes all checks.
i18n-check -a  # --all
i18n-check -CHECK_ID
```

<div id="progress" class="w-2/12"/>

---

# Configuration

```yaml
src-dir: frontend
i18n-dir: frontend/i18n
i18n-src: frontend/i18n/en.json
file-types-to-check: [.ts, .js] # .vue, .svelte, .jsx

checks:
  # Global configurations are applied to all checks.
  global:
    active: true # enables all checks by default
    directories-to-skip: [frontend/node_modules]
    files-to-skip: []
  key-formatting: # example individual check
    active: false # can be used to override individual checks
    keys-to-ignore: [] # regexes for ignoring keys
...
```

<div id="progress" class="w-3/12"/>

---

# Conventions

## Rules

- All keys must begin with `i18n.`
- The base path must be the file path where the key is used (multiple -> lowest common with `_global`)
- Base paths must be followed by a minimally descriptive content reference (only formatting checked)
- Separate directory paths with periods
- Separate directory / file name components and content references with underscores
- Repeated words in the file path, including the file name, must not be repeated in the key

## Example

- File: `components/component/ComponentName.ext`
- Key: `"i18n.components.component_name.content_reference"`

<div id="progress" class="w-4/12"/>

---

# Pass and Fail

<div class="flex justify-center space-x-24 py-6">
  <div class="flex flex-col items-center">
   <img src="/i18nCheckAllPass.gif" class="h-64" alt="GIF that shows all i18n-check checks passing"/>
   <p>All checks pass</p>
  </div>
  <div class="flex flex-col items-center">
    <img src="/i18nCheckAllFail.gif" class="h-64" alt="GIF that shows all i18n-check checks failing"/>
    <p>All checks fail</p>
  </div>
</div>

<div id="progress" class="w-5/12"/>

---
title: Checks
---

# Checks - 1/6

## `--key-formatting` (`-kf`)

- Does the source file contain keys that don't follow the required formatting rules?
- Includes `--fix` to fix formatting automatically

## `--key-naming` (`-kn`)

- Are key names consistent with how and where they are used in the codebase?
- Includes `--fix` to rename keys automatically

<div id="progress" class="w-6/12"/>

---
hideInToc: true
---

# Checks - 2/6

## `--nonexistent-keys` (`-nk`)

- Does the codebase include i18n keys that are not within the source file?
- Includes `--fix` to add keys interactively

## `--unused-keys` (`-uk`)

- Does the source file have keys that are not used in the codebase?
- Includes `--delete` to delete unused keys automatically

<div id="progress" class="w-7/12"/>

---
hideInToc: true
---

# Checks - 3/6

## `--non-source-keys` (`-nsk`)

- Do the target locale files have keys that are not in the source file?
- Includes `--delete` to delete non-source keys automatically

## `--repeat-keys` (`-rk`)

- Do any of localization files have repeat keys?

<div id="progress" class="w-8/12"/>

---
hideInToc: true
---

# Checks - 4/6

## `--repeat-values` (`-rv`)

- Does the source file have repeat values that can be combined into a single key?

## `--sorted-keys` (`-sk`)

- Are the i18n source and target locale files sorted alphabetically?
- Includes `--fix` to sort keys automatically

<div id="progress" class="w-9/12"/>

---
hideInToc: true
---

# Checks - 5/6

## `--nested-files` (`-nf`)

- Do the i18n files contain nested JSON structures? (warning)
- Includes `--fix` to flatten JSON files automatically

## `--missing-keys` (`-mk`)

- Are any keys from the source file missing in the locale files?
- Includes `--fix --locale ENTER_ISO_2_CODE` to add missing keys interactively

<div id="progress" class="w-10/12"/>

---
hideInToc: true
---

# Checks - 6/6

## `--aria-labels` (`-al`)

- For both LTR and RTL languages, do keys that end in `_aria_label` end in punctuation?
- Includes `--fix` to remove punctuation automatically

## `--alt-texts` (`-at`)

- For both LTR and RTL languages, are keys that end in `_alt_text` missing proper punctuation?
- Includes `--fix` to add periods automatically

<div id="progress" class="w-11/12"/>

---
hideInToc: true
---

# Thank you!

- Questions, comments and suggestions are very welcome :)

<div class="flex justify-center space-x-24 py-6">
  <div class="flex flex-col items-center">
   <img src="/i18nCheckQRCodeWhite.png" class="h-64" alt="QR code to GitHub:activist-org/i18n-check"/>
   <p>GitHub:activist-org/i18n-check</p>
  </div>
  <div class="flex flex-col items-center">
    <img src="/i18nCheckSlidesQRCode.png" class="h-64" alt="QR code to a markdown file for the slides"/>
    <p>Slides Content</p>
  </div>
</div>

<div id="progress" class="w-12/12"/>
