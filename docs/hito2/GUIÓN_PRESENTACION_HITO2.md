# Guion de presentación — Backend de FrescApp (Hito 2)

**Duración objetivo:** 7 minutos.  
**Orden sugerido:** demostración breve, explicación técnica, decisión de arquitectura y cierre.  
**Nota:** el CRUD de inventario ya se probó localmente en Postman; el guion deja el espacio para presentar también el CRUD de lista de compras cuando termine su verificación y la prueba en otro equipo.

## 0:00–0:35 · Apertura

> “En el Hito 1 definimos qué necesitaba FrescApp. En este hito construimos el motor que recibe solicitudes, valida quién las hace, aplica reglas y guarda los datos. Hoy mostraremos el backend con dos recursos: inventario y lista de compras.”

## 0:35–2:20 · Demostración Postman

**Integrante 1 comparte la colección local y muestra una petición a la vez.**

> “La colección se ejecuta contra Firebase Emulator Suite en este computador. No usamos una API externa ni datos de producción. Primero iniciamos sesión con una cuenta sintética del emulador; Postman conserva localmente el token que devuelve Auth Emulator.”

> “Para inventario enviamos POST para crear una manzana, GET para comprobar que quedó guardada, PATCH para cambiar la cantidad y DELETE para borrarla. Revisamos los estados: 201, 200, 200 y 204. El 204 confirma que el borrado terminó y por eso no trae cuerpo.”

> “Ahora repetimos el mismo ciclo en lista de compras. Es un recurso distinto, con su propia ruta y campos. Así demostramos que las cuatro operaciones funcionan en ambos recursos.”

**Si el CRUD de lista aún no se ha completado en ensayo:** no afirmar que ya está comprobado; mostrar las solicitudes de la colección y marcar su ejecución como siguiente evidencia.

## 2:20–3:20 · Recorrido por capas

**Integrante 2 muestra el diagrama de capas en la web y luego los archivos correspondientes.**

> “La petición entra por el router, que identifica recurso, método e ID. El controlador se ocupa del protocolo HTTP: token, entrada y respuesta. El servicio contiene reglas de dominio. El repositorio hace las consultas a Firestore. Así evitamos mezclar la respuesta HTTP con las reglas o las consultas.”

> “El servidor obtiene el UID del ID token verificado; no acepta el UID que mande el cliente. El repositorio limita la operación a las colecciones privadas de esa cuenta.”

## 3:20–4:20 · Persistencia y HTTP

**Integrante 3 explica estados y almacenamiento.**

> “Firestore es nuestra persistencia real; en la presentación usamos su emulador para que otra computadora pueda repetirla sin tocar producción. Las rutas son REST y están orientadas a recursos: `/v1/inventario` y `/v1/lista-compras`.”

> “Los estados de éxito no son todos iguales: 201 cuando se crea un registro, 200 para lecturas y actualizaciones, 204 al borrar. Cuando hay errores usamos códigos como 400 para entrada inválida, 401 si no hay un token válido y 404 si no existe la ruta o el registro.”

## 4:20–5:20 · Framework web y plataforma

**Integrante 4 usa la comparación interactiva de la presentación.**

> “Firebase Cloud Functions v2 es la plataforma donde corre y se expone el servicio. Express y Fastify son frameworks HTTP que podrían organizar las rutas dentro de esa plataforma. En este alcance usamos `onRequest` y un router propio: tenemos dos recursos y preferimos menos dependencias. El costo aceptado es mantener manualmente el despacho de rutas y el formato de errores.”

> “Si aumentan las rutas comunes o middleware, reevaluaríamos Express o Fastify. No los elegimos solo por popularidad; comparamos qué problema concreto resuelven en FrescApp.”

## 5:20–6:20 · Monolito modular

**Integrante 5 usa la comparación de arquitectura.**

> “La API es un monolito modular: un solo servicio publicable contiene los módulos de inventario y lista de compras, organizados por capas. Elegimos esto porque el equipo y la carga esperada son pequeños y ambos recursos comparten autenticación, Firestore y despliegue.”

> “Aceptamos que los dos recursos escalen y se publiquen juntos. Separaríamos servicios si uno necesitara despliegue, carga o disponibilidad independiente; en ese caso pagaríamos el costo de operar más servicios y coordinar la comunicación entre ellos.”

## 6:20–7:00 · Cierre

> “El resultado es una API REST propia, con persistencia en Firestore, autenticación, validación y capas separadas. La colección y el emulador permiten repetir la demostración. Como siguiente control de calidad, haremos la misma instalación y ambos CRUD en otro computador, guardando versiones, respuestas HTTP y capturas redactadas. Cada integrante puede explicar una parte del recorrido y el costo de una decisión.”

## Preparación de equipo

- Integrante 1: demostración y contrato Postman.
- Integrante 2: capas y una operación de código.
- Integrante 3: Firestore, autenticación y estados HTTP.
- Integrante 4: Cloud Functions, router propio, Express y Fastify.
- Integrante 5: monolito modular y escenarios para reevaluar.

Si el equipo tiene menos de cinco integrantes, unir bloques. Si tiene más, repartir demostración, errores HTTP, pruebas en otro equipo y modelo de datos.

