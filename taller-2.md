# Taller 2 Corte: React

Estudiante: Fredy Jarava
Asignatura: Desarrollo Frontend



## Punto 1. ¿Qué es React?

### ¿Qué es React y para qué sirve dentro del desarrollo web?

React es una librería de JavaScript pensada exclusivamente para construir interfaces de usuario de forma modular y eficiente. Su propósito principal en el desarrollo web actual es facilitar la creación de aplicaciones web de una sola página, conocidas como SPAs. Lo bueno es que es de codigo abierto y nos permite hacer uso de componentes reutilizable, es decir que se pueden agrupar de manera que podamos desarrollar interfaces interactivas de manera comoda.

En las páginas web tradicionales cada interacción o envío de formulario que se realizaba provocaba que la pantalla parpadeara porque el navegador tenía que solicitarle al servidor una página HTML completamente nueva. Con React esto no ocurre, ya que la aplicación carga una sola vez y cualquier cambio visual se maneja directamente en el cliente mediante JavaScript, modificando solo la parte específica de la pantalla que realmente cambió. Esto hace que la navegación sea mucho más rápida y fluida, similar a la experiencia de una aplicación de escritorio o de celular [1], [2].


### ¿Quién lo creó y en qué año apareció?

React fue creado por Jordan Walke, un ingeniero de software de Facebook. Este proyecto lo penso originamente como un prototipo llamado FaxJS, el se baso en las ideas de la programación funcional y en librerías del lenguaje XHP. La primera implementación en producción se hizo para el muro de noticias de Facebook en 2011 y despues se uso en Instagram en 2012. posteriormente Walke y el equipo de Facebook tomaron la decision de dejarlo de codigo abierto en mayo de 2013 durante la conferencia JSConf US [3].


### ¿Es una librería o un framework?

Se puede decir que React es una librería y no un framework. la gran diferencia es el control del flujo del programa y la libertad que tiene el desarrollador para estructurar la aplicación, es mas para desarrollos especificos ya que nos podemos enfocar solo en la vista, sin embargo un framework abarca mas aspectos del desarrollo web

Un framework, como Angular, impone una arquitectura muy rígida: define cómo organizar carpetas, cómo realizar el enrutamiento de páginas, cómo gestionar peticiones al servidor y cómo manejar los datos. En un framework se produce la inversión de control, es decir, el framework es quien toma el mando y llama al código del desarrollador. En contraste, React es una librería enfocada exclusivamente en la interfaz visual. React no te obliga a usar un enrutador ni una solución, aqui el desarrollador es quien mantiene el control del proyecto y puede elegir que herramienta quiere usar dependiendo de la necesidad, por ejemplo si queremos que la app tenga varias rutas podemos usar React Router para navegación o Redux para gestión de datos [4].


### ¿Qué significa que React sea declarativo?

Que React sea declarativo significa que el desarrollador describe qué aspecto visual debe tener la pantalla según los datos del momento, en lugar de escribir instrucciones paso a paso sobre cómo modificar manualmente cada elemento del navegador.

La interfaz se puede entender como una función directa del estado. Esto significa que cuando los datos de la aplicación cambian, únicamente se actualiza el estado y lo que hace React es encargarse de calcular las diferencias en memoria y redibujar a cada rato en pantalla solo las partes modificadas de manera automatica [5].


## Punto 2. ¿Qué problema resuelve React?

### Dificultad principal de construir interfaces manipulando el DOM a mano

Antes de la llegada de librerías como React, la construcción de interfaces dinámicas se hacía manipulando el DOM (Document Object Model) directamente con JavaScript tradicional o herramientas como jQuery, a través de instrucciones como document.getElementById(), appendChild() o innerHTML. Aunque este método funciona bien en proyectos pequeños de dos o tres botones, a medida que las aplicaciones creacian ya se cuando se agregaban mas elementos como carritos de compra, paneles de usuario, notificaciones y listas dinámicas, el código se vuelve difícil de mantener, lo que conllevaba a errores.

La manipulación manual del DOM generaba dos problemas principales:

1. **El primero era la pérdida de sincronización entre los datos y la pantalla:**  si un usuario agregaba un producto al carrito, era necesario actualizar la variable del total en la memoria de JavaScript y luego recordar buscar en el código el texto del carrito en el encabezado, el resumen de la compra y el botón flotante para modificar su valor a mano. Olvidar una sola línea de actualización dejaba la interfaz desfasada con la memoria, es decir podria pasar que se mostrara un valor incorrecto de los productos.

2. **El segundo problema era el rendimiento del navegador:** cada modificación directa sobre el DOM obliga al motor a recalcular estilos, volver a medir geometrías y redibujar la pantalla. Y repetir siempre esas operaciones hacía que las páginas se sintieran muy lentas y pesadas [6].


### Diferencia entre el enfoque imperativo y el enfoque declarativo

El enfoque imperativo consiste en indicarle al navegador paso a paso que es lo que debe hacer, como buscar el elemento en el documento, comprobar si existe, modificar su clase CSS, alterar el texto interno y agregarlo al contenedor.

En cambio, el enfoque declarativo describe únicamente el resultado final deseado en función del estado actual, es decir si el usuario está conectado, se muestra el botón verde con el texto Conectado; si no lo está, se muestra el botón gris con el texto Desconectado. El desarrollador se encarga de definir el resultado final y React se encarga de actualizar la interfaz automaticamente.

La diferencia se ilustra claramente en el siguiente ejemplo:

```javascript
// Enfoque imperativo con JavaScript tradicional
const boton = document.getElementById("boton-sesion");
if (usuarioConectado) {
  boton.className = "btn-verde";
  boton.innerText = "Conectado";
} else {
  boton.className = "btn-gris";
  boton.innerText = "Desconectado";
}
```

```jsx
// Enfoque declarativo con React
function BotonSesion({ usuarioConectado }) {
  return (
    <button className={usuarioConectado ? "btn-verde" : "btn-gris"}>
      {usuarioConectado ? "Conectado" : "Desconectado"}
    </button>
  );
}
```

En la versión de React no se le indica al navegador cómo buscar ni cómo alterar elementos manualmente, sino que simplemente se define el resultado visual dependiente del estado [5].


### Cómo ayuda React a mantener la interfaz sincronizada con los datos

Para mantener la pantalla siempre sincronizada con los datos sin afectar el rendimiento, React utiliza el Virtual DOM y su algoritmo de reconciliación. El Virtual DOM es una representación ligera de la interfaz que React mantiene en memoria como objetos JavaScript.

Cuando el estado o los datos de un componente cambian, React ejecuta el siguiente ciclo:
1. Genera un nuevo árbol virtual en memoria con la representación actualizada de la interfaz.
2. Compara este árbol nuevo con la versión previa mediante un algoritmo de diferenciación (diffing).
3. Calcula el conjunto mínimo de cambios necesarios y actualiza de manera atómica únicamente esos nodos en el DOM real del navegador.

Este mecanismo evita repintar elementos que no han cambiado y garantiza que la vista siempre refleje con exactitud los datos en memoria [7].


### Rol de los componentes reutilizables en la solución de ese problema

La solución de React se basa en la arquitectura de componentes reutilizables. En lugar de estructurar la aplicación en documentos HTML largos con bastante código, la interfaz se divide en piezas independientes. Cada componente gestiona su propia estructura, estilos y lógica interna.

Este enfoque ofrece ventajas concretas:
- Reduce la duplicación de código, permitiendo crear elementos estándar (botones, tarjetas, campos) y reutilizarlos en múltiples vistas.
- Simplifica la depuración: si surge un fallo en una sección puntual de la interfaz, se interviene únicamente el archivo de ese componente sin alterar el resto del sistema.
- Facilita el trabajo colaborativo, ya que varios desarrolladores pueden avanzar simultáneamente en componentes distintos sin generar conflictos en el código base [8].


## Punto 3. Principales componentes de React

Para construir aplicaciones en React se utilizan cinco conceptos fundamentales: los componentes, la sintaxis JSX, las props, el estado mediante useState y el manejo de eventos.


### 1. Componentes

Definición:
Los componentes son los bloques fundamentales de construcción en cualquier aplicación de React. En las versiones modernas corresponden a funciones de JavaScript que devuelven marcado visual estructurado y que pueden ser reutilizadas tanta veces como queramos y eso es lo bueno de react [2].

Características principales:
- Su nombre debe comenzar obligatoriamente con letra mayúscula, por ejemplo TarjetaUsuario o Encabezado, para distinguirse de las etiquetas nativas del navegador.
- Son modulares y componibles: pueden anidarse unos dentro de otros para formar pantallas complejas a partir de piezas sencillas.
- Reciben datos de entrada y retornan una descripción visual estructurada en JSX.

Ejemplo de código:

```jsx
function Saludo() {
  return (
    <article className="caja-saludo">
      <h2>Hola a todos</h2>
      <p>Este es un componente funcional reutilizable.</p>
    </article>
  );
}

export default Saludo;
```

Explicación del código:
La función Saludo define un componente que retorna un encabezado y un párrafo dentro de un contenedor. Para incluirlo en cualquier vista de la aplicación, simplemente se utiliza la etiqueta con su nombre: `<Saludo />`.


### 2. JSX (JavaScript XML)

Definición:
JSX es una extensión de la sintaxis de JavaScript que permite escribir estructuras similares a HTML directamente dentro del código del componente [9]. Durante la fase de compilación (a través de herramientas como Vite), este código se transforma en llamadas puras a funciones de JavaScript interpretables por el navegador.

Características principales y reglas básicas:
- Todo componente debe retornar un único elemento raíz. En caso de no requerir un contenedor visual adicional en el DOM, se puede utilizar un fragmento vacío `<>...</>`.
- Todas las etiquetas deben cerrarse de forma explícita, incluyendo las que en HTML tradicional eran autocontenidas, como `<input />` o `<img />`.
- Los nombres de los atributos se escriben en convención camelCase (por ejemplo, className en lugar de class, y htmlFor en lugar de for).
- Para evaluar variables o expresiones de JavaScript dentro del marcado, se encierran entre llaves `{}`.

Ejemplo de código:

```jsx
function TarjetaEstudiante() {
  const nombre = "Carlos Mendoza";
  const semestre = 6;

  return (
    <div className="tarjeta">
      <h3>Estudiante: {nombre}</h3>
      <p>Actualmente cursando semestre: {semestre}</p>
      <input type="text" placeholder="Escribe un comentario" />
    </div>
  );
}
```

Explicación del código:
Se aprecia la inserción de las variables nombre y semestre mediante llaves `{}`, el uso del atributo className para vincular estilos y el cierre explícito de la etiqueta `<input />`.


### 3. Props (Propiedades)

Definición:
Las props son las formas de comunicación utilizados para mandar datos desde un componente padre hacia un componente hijo [10]. Funcionan de manera similar a los argumentos de una función.

Características principales:
- Flujo unidireccional: la información desciende siempre desde los componentes padres hacia los componentes hijos.
- Inmutabilidad: son valores de solo lectura. El componente hijo no debe modificar directamente las props que recibe; únicamente las consume para renderizar la vista.
- Permiten parametrizar componentes para mostrar datos dinámicos conservando la misma estructura base.

Ejemplo de código:

```jsx
function TarjetaMateria({ materia, creditos }) {
  return (
    <div className="bloque-materia">
      <h4>{materia}</h4>
      <p>Número de créditos: {creditos}</p>
    </div>
  );
}

function Horario() {
  return (
    <section>
      <TarjetaMateria materia="Desarrollo Frontend" creditos={3} />
      <TarjetaMateria materia="Bases de Datos" creditos={4} />
    </section>
  );
}
```

Explicación del código:
El componente padre Horario invoca dos veces al componente hijo TarjetaMateria, suministrándole valores específicos para materia y creditos. El hijo recibe estos valores y los muestra en pantalla sin alterarlos.


### 4. Estado (useState)

Definición:
El estado representa la memoria interna de un componente, permitiendo almacenar datos que pueden variar a lo largo del tiempo debido a interacciones del usuario o respuestas de red [11].

Características principales:
- En componentes funcionales se administra a través del hook useState.
- Retorna un arreglo con dos elementos: la variable con el valor actual y una función despachadora encargada de actualizar dicho valor.
- Cada vez que se ejecuta la función de actualización, React programa un nuevo renderizado del componente para refrescar la interfaz con el dato más reciente.
- Cada instancia de un componente mantiene un estado completamente independiente.

Ejemplo de código:

```jsx
import { useState } from 'react';

function Contador() {
  const [clics, setClics] = useState(0);

  function aumentar() {
    setClics(clics + 1);
  }

  return (
    <div className="contador-caja">
      <p>Cantidad de clics: {clics}</p>
      <button onClick={aumentar}>Sumar un clic</button>
    </div>
  );
}
```

Explicación del código:
Se inicializa clics en cero mediante useState(0). Cuando el usuario presiona el botón, se dispara la función aumentar, que llama a setClics(clics + 1). React detecta la actualización y redibuja el valor numérico en pantalla.


### 5. Eventos (onClick, onChange)

Definición:
Los eventos son los mecanismos mediante los cuales un componente detecta y reacciona a las acciones realizadas por los usuarios en el navegador como al hacer clic, escribir o mover el cursor [12].

Características principales:
- Los identificadores de eventos se escriben en convención camelCase, como onClick en lugar de onclick, y onChange en lugar de onchange.
- Se asigna como valor la referencia a la función manejadora sin paréntesis (por ejemplo, onClick={mostrarAviso}). Si se colocaran paréntesis, la función se ejecutaría de inmediato durante el renderizado inicial en lugar de esperar la acción del usuario.
- React utiliza un sistema interno de eventos sintéticos (SyntheticEvent) que garantiza un comportamiento homogéneo en todos los navegadores modernos.

Ejemplo de código:

```jsx
import { useState } from 'react';

function FormularioSimple() {
  const [texto, setTexto] = useState('');

  function escribirTexto(e) {
    setTexto(e.target.value);
  }

  function mostrarAviso() {
    alert("Texto enviado: " + texto);
  }

  return (
    <div className="caja-formulario">
      <input 
        type="text" 
        value={texto} 
        onChange={escribirTexto} 
        placeholder="Escribe algo aquí..." 
      />
      <button onClick={mostrarAviso}>Enviar</button>
      <p>Texto capturado: {texto}</p>
    </div>
  );
}
```

Explicación del código:
Cada vez que el usuario teclea en el campo de entrada, el evento onChange ejecuta la función escribirTexto y actualiza el estado con el valor actual del input (e.target.value). Al presionar el botón, el evento onClick activa la función mostrarAviso y despliega una alerta con el texto almacenado.


## Punto 4. Importancia de React en la industria

### ¿Por qué tantas empresas eligen React para sus productos web?

El uso de React por parte de empresas tecnológicas es debido en gran medida a su modularidad y escalabilidad. 

Cuando una organización cuenta muchos ingenieros colaborando en una misma plataforma web, mantener archivos tradicionales de HTML y JavaScript resulta inviable. Con React, el producto se descompone en módulos pequeños y autónomos. Cada equipo puede responsabilizarse de una sección específica (por ejemplo, el módulo de facturación, el catálogo de productos o el sistema de autenticación) sin generar interferencias en el repositorio común.

Asimismo, la optimización que ofrece el Virtual DOM permite construir aplicaciones de respuesta instantánea y transiciones suaves, lo cual resulta crítico para la retención de usuarios en plataformas de comercio electrónico. Además, la predictibilidad de los componentes funcionales simplifica la implementación de pruebas automatizadas que aseguran la estabilidad del sistema ante nuevas versiones [13].


### ¿Qué aporta React al ecosistema de desarrollo?

React impulsó una transformación estructural en el desarrollo web moderno, sirviendo como base para herramientas y arquitecturas avanzadas.

A partir de su modelo de componentes surgieron frameworks de producción como Next.js y Remix. Estas herramientas potencian a React añadiendo renderizado en el servidor (Server-Side Rendering o SSR) y generación de sitios estáticos (Static Site Generation o SSG), lo que resuelve los tiempos de carga inicial y permite una indexación óptima por parte de los motores de búsqueda para posicionamiento SEO.

De igual forma, la necesidad de procesar JSX y optimizar paquetes impulsó el desarrollo de herramientas de compilación modernas y de alto rendimiento como Vite y Turbopack. Además, los mismos principios conceptuales de React se extendieron al desarrollo móvil mediante React Native, permitiendo construir aplicaciones nativas tanto para Android como para iOS utilizando la misma base de conocimiento y lógica de componentes [1], [4].


### ¿Qué papel juegan su comunidad y su mantenimiento?

El sostenimiento y la vigencia de React esta respaldado por grandes empresas y tambien cuenta con el apoyo de la comunidad de codigo abierto. La librería es coordinada y mantenida de forma continua por un equipo de ingenieros dedicados dentro de Meta, en colaboración con organizaciones de infraestructura web como Vercel y una extensa red global de desarrolladores independientes.

Al contar con una de las comunidades más activas del software libre, el registro de paquetes npm dispone de miles de soluciones probadas que abarcan librerías de diseño, gestión de formularios, animaciones y componentes accesibles. Del mismo modo, cualquier duda técnica o error común cuenta con abundante documentación oficial traducida, tutoriales actualizados y soporte colaborativo en foros especializados [3],[13].


### ¿Por qué es una habilidad relevante para un desarrollador frontend hoy en día?

En el mercado laboral contemporáneo, dominar React constituye una de las competencias más solicitadas dentro del desarrollo frontend. Las encuestas anuales de Stack Overflow y diversos análisis sobre contratación en la industria tecnológica sitúan a React de manera recurrente entre las tecnologías más demandadas por empresas a nivel mundial.

Más allá del volumen de oportunidades de empleo, aprender React proporciona fundamentos de ingeniería sólidos, como el flujo unidireccional de datos, la gestión de estados inmutables y la composición funcional. Estos principios son transferibles a múltiples herramientas modernas, permitiendo que un desarrollador que comprenda bien React pueda adaptarse con facilidad a alternativas como Vue, Svelte o Angular [13].


## Punto 5. Grandes empresas que utilizan React

Dos de los casos más representativos a nivel mundial que demuestran la capacidad de React para operar a gran escala en producción son Meta y Airbnb [14], [15].


### 1. Meta (Facebook e Instagram)

En qué producto o sección lo usan:
Meta utiliza React en las partes más críticas e interactivas de sus plataformas principales. En Facebook, la librería se encarga de gestionar el muro de noticias (News Feed), la bandeja de entrada de mensajes de Messenger en la versión web, el sistema de notificaciones en tiempo real y el panel publicitario para empresas llamado Meta Ads Manager. De igual manera, la versión web completa de la red social Instagram está desarrollada utilizando los componentes de React [14].

Por qué es un caso relevante:
Este caso es el más relevante de todos porque Meta es la cuna donde nació la tecnología. Hacia los años 2010 y 2011, los ingenieros de Facebook estaban teniendo dificultades serias para sincronizar las notificaciones de chat y las reacciones con millones de personas conectadas simultáneamente. Con frecuencia la campana de notificaciones mostraba mensajes no leídos cuando el chat ya estaba abierto, o la interfaz quedaba desactualizada. La implementación de React permitió manejar miles de cambios de datos concurrentes sin perder la coherencia visual. Al probar que React era capaz de operar con éxito ante la escala de Facebook e Instagram, se demostró ante la industria que el modelo de componentes declarativos y el Virtual DOM eran aptos para plataformas de máxima exigencia [14].


### 2. Airbnb (Plataforma mundial de reservas y alojamiento)

En qué producto o sección lo usan:
Airbnb implementa React en la totalidad de su plataforma web pública (airbnb.com). La librería está presente en el motor interactivo de búsqueda de hospedajes con mapas interactivos, en los calendarios dinámicos para consultar disponibilidad de fechas en tiempo real, en el proceso de reserva y pago en línea (checkout), y en el panel de administración que utilizan los anfitriones para gestionar sus propiedades y precios [15].

Por qué es un caso relevante:
Porque Airbnb fue una de las primeras grandes compañías de comercio electrónico y viajes que decidió migrar todo su sistema frontend a React. Antes de realizar esta modernización, la plataforma presentaba lentitud cuando los usuarios cambiaban fechas o aplicaban múltiples filtros de búsqueda sobre miles de alojamientos disponibles. Al implementar React junto a su modelo de componentes, lograron que las búsquedas, los filtros y la navegación entre habitaciones fueran prácticamente instantáneos sin recargar la pantalla, elevando las tasas de reserva completadas y mejorando la satisfacción de los viajeros en todo el mundo. Asimismo, la modularidad de los componentes le permitió a sus equipos de ingeniería mantener una interfaz consistente y sincronizada a gran escala en bastante idiomas y monedas [15].


## Referencias Bibliográficas

[1] React Core Team, "Aprende React: Describir la interfaz de usuario," Documentación Oficial de React, Meta Platforms, Inc., 2024. [En línea]. Disponible: https://es.react.dev/learn/describing-the-ui

[2] MDN Contributors, "Primeros pasos en React," MDN Web Docs, Mozilla Corporation, 2024. [En línea]. Disponible: https://developer.mozilla.org/es/docs/Learn_web_development/Core/Frameworks_libraries/React_getting_started

[3] Colaboradores de Wikipedia, "React," Wikipedia, La enciclopedia libre, 2024. [En línea]. Disponible: https://es.wikipedia.org/wiki/React

[4] M. Ángel Durán (midudev), "React: ¿biblioteca o framework?," midu.dev, 2023. [En línea]. Disponible: https://midu.dev/react-biblioteca-o-framework/

[5] ReactJS Wiki, "¿Qué significa exactamente que sea declarativo?," Comunidad ReactJS Wiki, 2024. [En línea]. Disponible: https://www.reactjs.wiki/que-significa-exactamente-que-sea-declarativo

[6] TrainingIT, "¿Qué es React y qué problema resuelve?," TrainingIT Blog, 2023. [En línea]. Disponible: https://www.trainingit.es/que-es-react/

[7] React Core Team, "Gestionar el estado," Documentación Oficial de React, Meta Platforms, Inc., 2024. [En línea]. Disponible: https://es.react.dev/learn/managing-state

[8] freeCodeCamp, "How to Build Reusable React Components," freeCodeCamp News, 2023. [En línea]. Disponible: https://www.freecodecamp.org/news/how-to-build-reusable-react-components/

[9] Coddy Tech, "JSX en React: sintaxis y reglas básicas," Coddy Tech Docs, 2024. [En línea]. Disponible: https://coddy.tech/docs/es/react/jsx

[10] ReactJS Wiki, "¿Qué son las props en React?," Comunidad ReactJS Wiki, 2024. [En línea]. Disponible: https://www.reactjs.wiki/que-son-las-props-en-react

[11] ReactJS Wiki, "¿Qué hace el hook useState?," Comunidad ReactJS Wiki, 2024. [En línea]. Disponible: https://www.reactjs.wiki/que-hace-el-hook-use-state

[12] ReactJS Wiki, "Cómo añadir un evento a un componente en React," Comunidad ReactJS Wiki, 2024. [En línea]. Disponible: https://www.reactjs.wiki/como-anadir-un-evento-a-un-componente-en-react

[13] Sophilabs, "Razones por las que React es tan popular," Sophilabs Blog, 2023. [En línea]. Disponible: https://sophilabs.com/es/articulos/razones-por-las-que-react-es-tan-popular

[14] GeeksforGeeks, "Top Companies Using ReactJS," GeeksforGeeks, 2024. [En línea]. Disponible: https://www.geeksforgeeks.org/reactjs/companies-that-use-react/

[15] JayDevs, "Top Companies Using React JS: Real-World Examples," JayDevs Blog, 2024. [En línea]. Disponible: https://jaydevs.com/top-companies-using-react-js/
