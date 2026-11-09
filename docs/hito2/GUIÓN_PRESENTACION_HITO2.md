# Guion de presentación — Backend de FrescApp (Hito 2)

**Duración objetivo:** 7 minutos.  
**Distribución:** tres integrantes, con bloques consecutivos y tiempos equilibrados.  
**Orden:** demostración, explicación técnica, decisiones de arquitectura y cierre.

**Nota de ensayo:** antes de presentar, ejecuten la colección en Postman y registren los resultados reales. No afirmen que una operación está comprobada si no la ejecutaron; si algo sigue pendiente, indíquenlo con claridad.

## 0:00–0:35 · Apertura — Integrante 1

> “En el Hito 1 definimos qué necesitaba FrescApp. En este hito construimos el motor que recibe solicitudes, valida quién las hace, aplica reglas y guarda los datos. Hoy mostraremos el backend con dos recursos: inventario y lista de compras.”

## 0:35–2:20 · Demostración en Postman — Integrante 1

**El integrante 1 comparte la colección local y muestra una petición a la vez.**

> “La colección se ejecuta contra Firebase Emulator Suite en este computador. No usamos APIs externas ni datos de producción. Primero iniciamos sesión con una cuenta sintética del emulador; Postman conserva localmente el token que devuelve Auth Emulator.”

> “Para inventario enviamos POST para crear una manzana, GET para comprobar que quedó guardada, PATCH para cambiar la cantidad y DELETE para borrarla. Revisamos los estados: 201, 200, 200 y 204. El 204 confirma que el borrado terminó y por eso no trae cuerpo.”

> “Ahora repetimos el ciclo en lista de compras. Es un recurso distinto, con su propia ruta y campos. Así mostramos las cuatro operaciones en ambos recursos.”

**Si el CRUD de lista de compras aún no se ha ensayado, no lo presenten como comprobado:** indiquen que falta esa ejecución y muestren el resultado cuando la hayan completado.

## 2:20–3:20 · Capas — Integrante 2

**El integrante 2 muestra el diagrama de capas y los archivos correspondientes.**

> “La petición entra por el router, que identifica el recurso, el método y el ID. El controlador se ocupa del protocolo HTTP: token, entrada y respuesta. El servicio contiene las reglas del dominio. El repositorio hace las consultas a Firestore. Así evitamos mezclar la respuesta HTTP con las reglas o las consultas.”

> “El servidor obtiene el UID del ID token verificado; no acepta el UID que mande el cliente. El repositorio limita la operación a las colecciones privadas de esa cuenta.”

## 3:20–4:20 · Persistencia y HTTP — Integrante 2

> “Firestore es nuestra persistencia. Para la demostración usamos su emulador, de modo que se pueda repetir sin tocar producción. Las rutas REST están orientadas a recursos: /v1/inventario y /v1/lista-compras.”

> “Los estados de éxito dependen de la operación: 201 al crear, 200 al leer o actualizar y 204 al borrar. Para los errores usamos, por ejemplo, 400 si la entrada es inválida, 401 si falta un token válido y 404 si no existe la ruta o el registro.”

## 4:20–5:20 · Framework web y plataforma — Integrante 3

**El integrante 3 usa la comparación interactiva de la presentación.**

> “Firebase Cloud Functions v2 es la plataforma donde corre y se expone el servicio. Express y Fastify son frameworks HTTP que podrían organizar las rutas dentro de esa plataforma. En este alcance usamos onRequest y un router propio: tenemos dos recursos y preferimos mantener pocas dependencias. El costo que aceptamos es mantener manualmente el despacho de rutas y el formato de errores.”

> “Si aumentan las rutas comunes o el middleware, reevaluaríamos Express o Fastify. No los elegimos solo por popularidad; comparamos qué problema concreto resolverían en FrescApp.”

## 5:20–6:20 · Monolito modular — Integrante 3

**El integrante 3 usa la comparación de arquitectura.**

> “La API es un monolito modular: un solo servicio publicable contiene los módulos de inventario y lista de compras, organizados por capas. Elegimos esto porque el equipo y la carga esperada son pequeños, y ambos recursos comparten autenticación, Firestore y despliegue.”

> “Aceptamos que los dos recursos escalen y se publiquen juntos. Separaríamos servicios si uno necesitara despliegue, carga o disponibilidad independiente. En ese caso también tendríamos que operar más servicios y coordinar su comunicación.”

## 6:20–7:00 · Cierre — Integrante 1

> “El resultado es una API REST propia, con persistencia en Firestore, autenticación, validación y capas separadas. La colección y el emulador permiten repetir la demostración. También dejamos documentada la decisión de arquitectura y sus costos. Gracias.”

## Reparto para tres integrantes

- **Integrante 1:** apertura, demostración en Postman y cierre.
- **Integrante 2:** capas, persistencia, autenticación y estados HTTP.
- **Integrante 3:** plataforma, comparación de frameworks y decisión monolito modular.

## Preparación del equipo

- Ensayar la presentación completa con cronómetro y respetar los siete minutos.
- Confirmar antes de exponer que los emuladores están iniciados y que Postman apunta al entorno local.
- Usar datos sintéticos y ocultar tokens, contraseñas y datos personales en pantalla.
- Cada integrante debe poder explicar su bloque y responder cómo se conecta con las capas del backend.
