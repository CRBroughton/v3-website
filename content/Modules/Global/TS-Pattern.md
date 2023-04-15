# TS-Pattern

V3 includes the [TS-Pattern library](https://github.com/gvergnaud/ts-pattern), useful for safely pattern-matching. Below
is an example of a [tRPC](https://trpc.io/) query response being pattern-matched against.

``` typescript
const createUser = async (input: User) => {
  const { type, error, data } = await $client.user.createUser.mutate(input)

  match(type)
    .with(
      'error',
      () => { throw new Error(error?.message) },
    )
    .with(
      'ok',
      () => { user.value = data! },
    )
    .exhaustive()
}
```