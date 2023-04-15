---
title: "Getting Started"
description: "Let's learn how to use my amazing module."
---

# Getting started with V3

## Prerequisties

### Github account

If you have a Github account, visit the following link to create a V3 repository:

https://github.com/CRBroughton/V3/generate

Then you can clone down your V3 repository.

### Alternative method

Alternatively, clone the repository down from github:

::code-group
  ```bash [git]
  git clone https://github.com/crbroughton/v3
  ```
::

Then CD into the folder you've just created and install the dependencies:

::code-group
  ```bash [pnpm]
  cd v3 && pnpm i
  ```
::

You'll then want to remove the .git folder to start your own project.

::code-group
  ```bash [pnpm]
  rm -rf .git
  ```
::
