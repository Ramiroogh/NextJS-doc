# Adapter, PrismaClient en NextJS
Al trabajar en Next js, vamos a tener un problema con el adapter, y es que cada vez que recarguemos nuestra aplicacion, tambien se Re-conectará de nuevo el cliente de prisma en nuestra aplicacion, y esto afectara nuestro modo de desarrollo, aqui hay una explicacion de la documentacion oficial:
[Best practice for instantiating PrismaClient with Next.js](https://www.prisma.io/docs/orm/more/help-and-troubleshooting/help-articles/nextjs-prisma-client-dev-practices)

### Error tipico
Este error nos vamos a encontrar cuando trabajemos con Prisma en una aplicacion con Next js:
```warn(prisma-client) There are already 10 instances of Prisma Client actively running.```

### Contexto
En desarrollo, el comando ```next dev``` borra la caché de Node.js en ejecución. Esto, a su vez, **inicializa una nueva instancia de PrismaClient cada vez debido a la recarga activa que crea una conexión con la base de datos**. Esto puede agotar rápidamente las conexiones de la base de datos, ya que *cada instancia de PrismaClient tiene su propio grupo de conexiones*.

---
## Solucion
La solución en este caso es crear una instancia única de PrismaClient y guardarla en el objeto **globalThis**. A continuación, mantenemos una comprobación para crear una instancia de PrismaClient solo si no está en el objeto globalThis, de lo contrario, volver a usar la misma instancia si ya está presente para evitar la creación de instancias adicionales de PrismaClient.

``` typescript
import { PrismaClient } from '@prisma/client'

const prismaClientSingleton = () => {
  return new PrismaClient()
}

declare global {
  var prisma: undefined | ReturnType<typeof prismaClientSingleton>
}

const prisma = globalThis.prisma ?? prismaClientSingleton()

export default prisma

if (process.env.NODE_ENV !== 'production') globalThis.prisma = prisma
```
Puede ampliar Prisma Client mediante una extensión de Prisma Client anexando el método de cliente $extends al crear una instancia de Prisma Client de la siguiente manera:

``` typescript
import { PrismaClient } from '@prisma/client'

const prismaClientSingleton = () => {
  return new PrismaClient().$extends({
    result: {
      user: {
        fullName: {
          needs: { firstName: true, lastName: true },
          compute(user) {
            return `${user.firstName} ${user.lastName}`
          },
        },
      },
    },
  })
}
```
Después de crear este archivo, ahora puede importar la instancia extendida de PrismaClient en cualquier lugar de sus páginas Next.js de la siguiente manera:
``` typescript
// e.g. in `pages/index.tsx`
import prisma from './db'

export const getServerSideProps = async () => {
  const posts = await prisma.post.findMany()

  return { props: { posts } }
}
```