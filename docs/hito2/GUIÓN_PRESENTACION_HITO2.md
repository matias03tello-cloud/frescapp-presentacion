# Guion breve — Presentación del backend FrescApp

**Duración:** 7 minutos · **Equipo:** 3 integrantes.

La pantalla interactiva de Postman es didáctica. La demostración A1 se realiza en Postman real contra Firebase Emulator Suite, con datos sintéticos.

## 0:00–0:20 · Apertura — Integrante 1

> “En el Hito 1 definimos FrescApp. En el Hito 2 construimos el backend que recibe solicitudes, valida al usuario y guarda sus datos. Hoy mostraremos inventario y lista de compras.”

## 0:20–2:30 · CRUD en vivo — Integrante 1

> “Usamos Postman contra los emuladores locales, sin APIs externas ni datos de producción. Primero iniciamos sesión con una cuenta sintética para obtener el token.”

> “En inventario creamos, consultamos, actualizamos y eliminamos un alimento. Se esperan los estados 201, 200, 200 y 204. Repetimos el mismo ciclo en lista de compras para comprobar el segundo recurso.”

Mostrar el estado HTTP y la respuesta de cada petición. No afirmar que un paso pasó si no se ve el resultado.

## 2:30–3:25 · Capas — Integrante 2

> “La ruta recibe la petición; el controlador valida identidad y prepara la respuesta; el servicio aplica las reglas del dominio; el repositorio consulta Firestore. El servidor obtiene el UID del token verificado y limita cada registro a su dueño.”

## 3:25–4:15 · Persistencia y HTTP — Integrante 2

> “Firestore conserva los datos. Las rutas REST son `/v1/inventario` y `/v1/lista-compras`. Respondemos 201 al crear, 200 al leer o actualizar y 204 al borrar. Usamos 400 para datos inválidos, 401 para una sesión no válida y 404 si no existe la ruta o el registro.”

## 4:15–5:20 · Tecnologías — Integrante 3

> “Elegimos JavaScript sobre Node.js 22 porque es el runtime configurado para Functions y trabaja con los SDK de Firebase del proyecto. Como JavaScript tiene tipado dinámico, validamos las entradas. Cloud Functions v2 ejecuta `onRequest` bajo demanda; aceptamos depender de Firebase y su plan facturado en producción.”

> “Para estas rutas elegimos un router propio y evitamos otra dependencia. Aceptamos mantener manualmente el despacho y los errores. Express ofrece rutas y middleware; Fastify agrega plugins y esquemas. Los reconsideraríamos si crecen las rutas comunes o las validaciones.”

## 5:20–6:20 · Arquitectura — Integrante 3

> “Elegimos un monolito modular: inventario y lista de compras comparten despliegue, autenticación y base de datos. Para el equipo y la carga actuales, reduce operación. El costo es que ambos módulos escalan y se publican juntos. Separaríamos servicios si necesitaran despliegue o carga independientes.”

## 6:20–7:00 · Cierre — Integrante 1

> “Construimos una API REST propia con dos recursos CRUD, capas separadas, autenticación y persistencia real. La colección permite repetir las pruebas con emuladores y datos sintéticos. Gracias.”

## Reparto y preparación

- **Integrante 1:** apertura, demostración Postman y cierre.
- **Integrante 2:** capas, Firestore, identidad y estados HTTP.
- **Integrante 3:** Node.js, Cloud Functions, router, alternativas y monolito modular.
- Ensayen los siete minutos con ambos CRUD; inicien antes los emuladores y oculten tokens y contraseñas.
- Cada integrante debe poder explicar una ruta y el costo de una decisión técnica.
