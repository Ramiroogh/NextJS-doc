# ReactNode, en NextJS & TypeScript

En TypeScript, cuando ves `ReactNode`, estás tipando el prop para que pueda aceptar cualquier cosa que sea renderizable por React. `ReactNode` es un tipo que incluye todos los tipos posibles que React puede representar y renderizar.

En este código:

```typescript
import { ReactNode } from "react"

const MaxWidthWrapper = ({
    className,
    children
}: {
    className?: string
    children: ReactNode
}) => {
    return (
        <div className="mx-auto w-full max-w-screen-xl px-2.5 md:px-20">{children}</div>
    )
}
export default MaxWidthWrapper
```

La prop `children` está siendo tipada como `ReactNode`. Esto significa que `children` puede ser cualquier cosa que pueda ser renderizada por React: un componente de React, una cadena de texto, un número, un fragmento, etc.

Esta flexibilidad es útil porque permite que el componente `MaxWidthWrapper` envuelva cualquier contenido que sea renderizable por React sin restricciones específicas sobre su tipo.

Cuando trabajas con TypeScript y React, es común usar `ReactNode` para las props de `children` cuando no quieres imponer restricciones específicas sobre qué tipo de contenido puede tener un componente.