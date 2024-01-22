# usePathname
El hook especial de navegación de Next.js llamado usePathname() se utiliza para leer la ruta actual del URL. Este hook se utiliza dentro de un componente de cliente y permite realizar ajustes dinámicos basados en la ruta actual. Al utilizar usePathname(), puedes condicionalmente renderizar componentes o ajustar estilos según la ruta actual.

Veamos un ejemplo del uso de este hook, para aplicar estilos dinamicos a los enlaces de un componente navbar:
```typescript
"use client"
import Link from "next/link";
import { usePathname } from "next/navigation";

const links = [
    {name: 'Home', href: '/'},
    {name: 'Laptop', href: '/Laptop'},
    {name: 'Smartphone', href: '/Smartphone'}
]

export default function Navbar() {
    const pathname = usePathname();

    return (
        <header className="mb-8 border-b">
            <div className="flex items-center justify-between mx-auto max-w-2xl px-4 sm:px-6 lg:max-w-7xl">
                <Link href='/'>
                    <h2 className="text-4xl font-bold">
                    Tech<span className="text-primary">One</span>
                    </h2>
                </Link>

                <nav className="hidden gap-12 lg:flex 2xl:ml-16">
                    {links.map((link, index) => (
                        <div key={index}>
                            {pathname === link.href ? (
                                <Link href={link.href} className="text-lg font-semibold text-primary">
                                    {link.name}
                                </Link>
                            ) : (
                                <Link href={link.href} className="text-lg font-semibold text-gray-600">
                                    {link.name}
                                </Link>
                            )}
                        </div>
                    ))}
                </nav>
            </div>
        </header>
    )
}
```


Aquí está el fragmento de código relevante:

```jsx
{links.map((link, index) => (
    <div key={index}>
        {pathname === link.href ? (
            <Link href={link.href} className="text-lg font-semibold text-primary">
                {link.name}
            </Link>
        ) : (
            <Link href={link.href} className="text-lg font-semibold text-gray-600">
                {link.name}
            </Link>
        )}
    </div>
))}
```
El hook `usePathname()` en el código que proporcionaste se utiliza para obtener la ruta actual del URL y aplicar estilos diferentes a los enlaces activos en la barra de navegación.

En el código, se importa el hook `usePathname()` de `next/navigation` y se utiliza para obtener la ruta actual del URL en la variable `pathname`. Luego, se itera sobre la matriz `links` y se renderizan los enlaces en la barra de navegación. Para cada enlace, se verifica si la ruta actual (`pathname`) coincide con la ruta del enlace (`link.href`). Si hay una coincidencia, se aplica un estilo diferente al enlace para resaltarlo como activo.



Si `pathname` coincide con `link.href`, se aplica la clase CSS `"text-lg font-semibold text-primary"` al enlace, lo que le da un estilo diferente. De lo contrario, se aplica la clase CSS `"text-lg font-semibold text-gray-600"` para el estilo predeterminado.

Esta es una forma común de utilizar el hook `usePathname()` para aplicar estilos a los enlaces activos en una barra de navegación en Next.js.