# Rutas Dinamicas []

En Next.js, las rutas dinámicas se utilizan para crear rutas que contienen parámetros variables en lugar de rutas estáticas fijas. Estos parámetros variables se pueden utilizar para generar páginas dinámicas con contenido único basado en los valores de los parámetros.

En el ejemplo que mencionas, la estructura de la ruta es `blog/slug[]/page.tsx`. La parte `[]` indica que el segmento de la ruta puede contener uno o más valores. Esto permite crear rutas dinámicas que pueden tener múltiples segmentos variables.

+ Por ejemplo, si tienes una página de blog y deseas mostrar diferentes publicaciones según el slug (un identificador único para cada publicación), puedes utilizar una ruta dinámica como `blog/[slug]/page.tsx`. Esto te permitiría generar páginas únicas para cada publicación en función de su slug.
---
## La clave, Los Corchetes []
Al utilizar los corchetes `[]`, Next.js reconoce que esa parte de la ruta es dinámica y puede contener diferentes valores en cada solicitud. Luego, puedes acceder a estos valores en tu componente de página utilizando el objeto `router` proporcionado por Next.js.

---
¡Claro! Aquí tienes un ejemplo de cómo podrías implementar una ruta dinámica en Next.js utilizando corchetes `[]`:

Supongamos que tienes una página de blog y deseas mostrar diferentes publicaciones según su slug. Primero, crea un archivo llamado `[slug].tsx` en la carpeta `pages/blog`. El nombre del archivo entre corchetes indica que es una ruta dinámica y el parámetro `slug` es el valor variable que utilizaremos.

```jsx
// pages/blog/[slug].tsx

import { useRouter } from 'next/router';

function BlogPost() {
  const router = useRouter();
  const { slug } = router.query;

  return (
    <div>
      <h1>Detalles del blog: {slug}</h1>
      {/* Aquí puedes mostrar los detalles del blog según el slug */}
    </div>
  );
}

export default BlogPost;
```
## Ejemplo:
En este ejemplo, utilizamos el hook `useRouter` de Next.js para acceder a la información de la ruta. `router.query` contiene los parámetros de la URL, y en este caso, estamos extrayendo el valor del parámetro `slug`. Luego, podemos utilizar ese valor para mostrar los detalles del blog específico.

Por ejemplo, si accedes a la URL `/blog/mi-publicacion`, el componente `BlogPost` mostrará "Detalles del blog: mi-publicacion".

+ Recuerda que debes asegurarte de tener configurado el enrutamiento adecuado en tu archivo `next.config.js` para que las rutas dinámicas funcionen correctamente.