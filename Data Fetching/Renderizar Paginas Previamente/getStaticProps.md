# Pre-Cargar paginas desde el Servidor
Veremos un  ejemplo de cómo cargar todas las páginas de una aplicación desde el servidor cuando un usuario visita la página por primera vez. Esto crea la ilusión de que la aplicación es rápida, ya que todas las páginas ya están cargadas en el DOM del navegador y listas para ser exploradas por el usuario.

+ Aqui esta la [Documentacion](https://nextjs.org/docs/pages/building-your-application/data-fetching/get-static-props) Oficial que habla sobre esto.

En Next.js, puedes lograr esto utilizando la función getStaticProps en lugar de getServerSideProps. La función getStaticProps se ejecuta en el momento de la compilación y permite generar páginas estáticas pre-renderizadas.

---
### Pages / index.tsx
```typescript
// Esta función se ejecuta en el momento de la compilación
export async function getStaticProps() {
  // Aquí puedes realizar cualquier lógica necesaria, como obtener datos de una API o una base de datos

  // Por ejemplo, obtendremos una lista de usuarios
  const res = await fetch('https://api.example.com/users');
  const data = await res.json();

  // Devolvemos los datos obtenidos como props
  return {
    props: {
      users: data,
    },
  };
}

// Componente de la página
export default function Home({ users }) {
  return (
    <div>
      <h1>Lista de usuarios:</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
}
```
### Explicación
En este ejemplo, la función ``getStaticProps`` se ejecutará en el momento de la compilación y obtendrá una lista de usuarios desde una API. Luego, los datos obtenidos se pasan como props al componente Home, que se renderizará en el cliente con los datos pre-cargados.

De esta manera, cuando un usuario visite la página por primera vez, todas las páginas ya estarán cargadas en el DOM del navegador, lo que proporcionará una experiencia de carga rápida.