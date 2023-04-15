# Authentication

By default, V3 is configured to use [Auth0]([Auth0](https://auth0.com)) for secure
authentication. Users who sign into your V3 application will be synced to your local
Prisma database, enabling you to perform typical database interactions.

V3 with look at your environment configure file (.env) for the below values:


```
AUTH_ORIGIN="http://localhost:3000"
NUXT_AUTH0_CLIENT_ID=""
NUXT_AUTH0_CLIENT_SECRET=""
NUXT_AUTH0_ISSUER=""
```

To populate these values, create an [Auth0]([Auth0](https://auth0.com)) application.

These same values will need to be set for your production instance; It's recommended
to set up separate development and production [Auth0]([Auth0](https://auth0.com)) applications.

They will then be read by the `api/auth/[...].ts` file, which is shown below.

```typescript
export default NuxtAuthHandler({
  adapter: PrismaAdapter(prisma),
  secret: envConfig.NUXT_SECRET,
  providers: [
    // @ts-expect-error You need to use .default here for it to work during SSR. May be fixed via Vite at some point
    Auth0Provider.default({
      clientId: envConfig.NUXT_AUTH0_CLIENT_ID,
      clientSecret: envConfig.NUXT_AUTH0_CLIENT_SECRET,
      issuer: envConfig.NUXT_AUTH0_ISSUER,
    }),
  ],
})
```


## Alternative authentication methods

V3 uses [Nuxt-auth](https://nuxt.com/modules/nuxt-auth), which provides a Nuxt-compatible
wrapper around [NextAuth.js](https://next-auth.js.org); Any of the [providers
listed there](https://next-auth.js.org/providers/) should work with V3.