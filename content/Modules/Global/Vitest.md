# Vitest

Vitest provides the ability to test both your front-end and back-end code.

V3 provides a mocked Prisma client, enabling testing of your
tRPC API without the need to directly access the database.

```typescript
import type { PrismaClient } from '@prisma/client'
import { beforeEach } from 'vitest'
import { mockDeep, mockReset } from 'vitest-mock-extended'

// Mocked Prisma client
const prismaMock = mockDeep<PrismaClient>()

export default prismaMock

beforeEach(() => {
  mockReset(prismaMock)
})
```

The mocked Prisma client can be used to resolve values
you would expect back from the API:

```typescript
test('getUsers Procedure - Returns a list of registered users', async () => {
    // Resolve a mocked user
    prisma.user.findMany.mockResolvedValue([testUser])

    // Call the mock procedure
    const response = await testPublicProcedures().user.getUsers()

    type UserResponse = inferProcedureOutput<AppRouter['user']['getUsers']>

    const expectation: UserResponse = {
        type: 'ok',
        data: [testUser],
    }

    expect(response).toEqual(expectation)
})

```