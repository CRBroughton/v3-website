---
title: "Getting Started"
description: "Let's learn how to use my amazing module."
---

# Getting started with V3

Please note, that the V3 documentation is currently a work in progress;
If you're in doubt, check the relevant documentation for the specific technology
for your needs.

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

## Setting up your V3 application

### Environment file

It's first recommended to take some time going over your basic configuration.
V3 is an opinionated meta-framework and assumes that the practices layed out
in the documentation are followed, however as V3 is also a template, you're
free to adjust it to meet your own requirements.

First copy the `.env.example` file to create your own `.env` configuration file;
This will be needed to provide V3 with the various values it will expect for
you to get started.

V3 type-checks your `.env` file to ensure that the file is correctly filled out
in case of user error (these checks are also performed for production instances).
If you wish to completely remove any of the values stored in your `.env` file,
you'll also need to remove the values from the `envConfig.ts` file so they are
no longer type-checked; Note that doing so may cause certain functionality to break
(authentication, database connections) and may require additional modifications
elsewhere in the template to fully remove a feature.

A successful configuration should look something like:

```
# __     _______   ____ _____  _    ____ _  __
# \ \   / /___ /  / ___|_   _|/ \  / ___| |/ /
#  \ \ / /  |_ \  \___ \ | | / _ \| |   | ' / 
#   \ V /  ___) |  ___) || |/ ___ \ |___| . \ 
#    \_/  |____/  |____/ |_/_/   \_\____|_|\_\
#

# TRPC SERVER URL
VITE_TRPC_URL="http://localhost:5000/trpc"
# POSTGRES VARIABLES
DATABASE_URL="postgresql://MyUser:MyPassword@localhost:5432/MyDatabaseName?schema=public"
DATABASE_NAME=MyDatabaseName
DATABASE_USER=MyUser
DATABASE_PASSWORD="G8L4j9FbhpC4rXk6McaK6aNLTQNi67G"
# AUTH0 AUTHENTICATION VARIABLES
# NUXT_SECRET - run: 'openssl rand -base64 64' to create a new key
NUXT_SECRET="ViT6Yrackd6ooQfdQXJx92L592ZsLTd"
AUTH_ORIGIN="http://localhost:3000"
NUXT_AUTH0_CLIENT_ID="PNaJzSBFr8GWoVz9j5PCLnZUcK3LoAF"
NUXT_AUTH0_CLIENT_SECRET="XXXXXXXXXXXXXXXXXXXXXXX-XXXXXXXXXXXXXX-XXXXXXXXXXXXXXXXXXXXXXXXX"
NUXT_AUTH0_ISSUER="https://dev-XXXXXXXXXXXXXXXX.uk.auth0.com"
```

If you have succesfully configured V3, you'll succesfully pass the `.env` type-checker
and see the welcome screen.

### Nuxt configuration

A Nuxt secret key can be provided to the `.env` file using the recommended `openssl`
command, which you can find in the `.env.example` file.

### Database configuration

V3 by default uses a SQLite database, however I have also provided the boilerplate
to use a PostgreSQL database as well. If you wish to use this, simply navigate to the
`prisma/schema.prisma` file and uncomment the following lines:

```
// datasource db {
//   provider = "postgresql"
//   url      = env("DATABASE_URL")
// }
```

then remove the following lines:

```
datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}
```

V3 will now use the provide PostgreSQL database, which you can configure inside
the `.env` file to your liking, and started with `docker compose up -d`.

### Authentication configuration

V3 by default uses [Auth0]((https://auth0.com)) to authenticate your users,
and expects you to provide a set of [Auth0]((https://auth0.com)) variables.
More information about [Auth0]((https://auth0.com)) for V3 can be found in
the [Authentication page](./Modules/Backend/Authentication.md).  