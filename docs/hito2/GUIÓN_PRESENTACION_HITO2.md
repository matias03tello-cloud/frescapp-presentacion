# Guion de presentación — Backend de FrescApp (Hito 2)

**Duración objetivo:** 7 minutos.  
**Distribución:** tres integrantes.  
**Orden:** demostración, capas, tecnologías y decisión de arquitectura.

**Ensayo:** practiquen con la colección local y muestren las respuestas reales. La pantalla interactiva “Explora una petición” es didáctica, no reemplaza Postman.

## 0:00–0:20 · Apertura — Integrante 1

> “En el Hito 1 definimos qué necesitaba FrescApp. En el Hito 2 construimos el backend que recibe solicitudes, valida la identidad y guarda los datos. Hoy mostraremos inventario y lista de compras.”

## 0:20–2:30 · Demostración en Postman — Integrante 1

**Antes de iniciar el cronómetro:** levanten los emuladores y ejecuten la solicitud "0. Crear cuenta local y guardar token". Así Postman tendrá un token sintético listo para las peticiones CRUD.

> “La colección apunta a Firebase Emulator Suite local. La autenticación usa 127.0.0.1:9099 y la API 127.0.0.1:5001; no usamos APIs externas ni producción.”

> “En inventario ejecutamos POST, GET por ID, PATCH y DELETE. Después repetimos esas cuatro operaciones en lista de compras. Comprobamos 201 al crear, 200 al leer o actualizar y 204 al borrar.”

**Orden exacto de la colección:**
- Inventario: solicitudes 1, 2, 3 y 4.
- Lista de compras: solicitudes 6, 8, 9 y 10. La solicitud 7 lee toda la colección y es opcional si falta tiempo.
- Muestren el estado HTTP y la respuesta. No dejen visible el token ni la contraseña.

## 2:30–3:25 · Capas — Integrante 2

> “El router reconoce método y ruta. El controlador verifica el token, valida la entrada HTTP y prepara la respuesta. El servicio aplica reglas de FrescApp. El repositorio concentra las consultas a Firestore. El UID se obtiene del token verificado, nunca del cuerpo enviado por el cliente.”

## 3:25–4:10 · Persistencia y HTTP — Integrante 2

> “Firestore conserva los datos en las subcolecciones de cada usuario. Usamos 201 al crear, 200 al leer o actualizar y 204 al borrar. Para errores respondemos 400 si los datos son inválidos, 401 si falta una sesión válida y 404 si la ruta o el registro no existe.”

## 4:10–5:30 · Tecnologías y motivo — Integrante 3

> “El servicio está escrito en JavaScript sobre Node.js 22. Elegimos ese runtime porque ya está configurado para Firebase Functions y comparte los SDK del proyecto. JavaScript tiene tipado dinámico; por eso validamos explícitamente cada entrada.”

> “Cloud Functions v2 ejecuta onRequest y publica la API por HTTPS bajo demanda. Reutiliza Authentication, Firestore y los emuladores, así no mantenemos otro servidor. El costo es depender de Firebase y habilitar facturación al desplegar en producción.”

> “Para dos recursos usamos un router propio y evitamos una dependencia adicional. Aceptamos mantener el despacho y los errores. Express resuelve rutas y middleware comunes; Fastify añade plugins y esquemas. Los evaluaríamos de nuevo si crecen las rutas o validaciones compartidas.”

## 5:30–6:30 · Monolito modular — Integrante 3

> “Inventario y lista de compras viven en un solo servicio, separados por capas. Elegimos el monolito modular porque el equipo es pequeño y ambos recursos comparten autenticación y base de datos. Reducimos despliegues y operación; aceptamos que los módulos escalen juntos. Separaríamos servicios si necesitaran carga o despliegue independientes.”

## 6:30–7:00 · Cierre — Integrante 1

> “El resultado es una API REST propia, con dos recursos CRUD, autenticación, capas separadas y persistencia real en Firestore. La colección permite repetir la demostración localmente. Gracias.”

## Reparto

- **Integrante 1:** apertura, Postman y cierre.
- **Integrante 2:** capas, persistencia, autenticación y estados HTTP.
- **Integrante 3:** tecnologías, alternativas y monolito modular.

## Preparación de Postman antes de exponer

1. Desde la raíz del proyecto, iniciar Auth, Firestore y Functions Emulator:
   npx firebase emulators:start --only auth,firestore,functions --project demo-frescapp-hito2
2. En la colección local, confirmar authUrl = http://127.0.0.1:9099 y baseUrl = http://127.0.0.1:5001/demo-frescapp-hito2/southamerica-west1/api. Mantener la colección sin compartir ni sincronizar.
3. Asignar una contraseña sintética a la variable local password. La variable email de ejemplo es hito2@frescapp.test; si ya existe en el emulador, usar otro correo sintético.
4. Ejecutar la solicitud 0. La colección guarda el ID token y UID; los POST guardan inventarioId y compraId.
5. Revisar manualmente los estados HTTP. Los scripts de la colección guardan tokens e IDs, pero no validan automáticamente los códigos de respuesta.
6. Si ven identitytoolkit.googleapis.com en la ruta de autenticación, comprueben el host: la variable authUrl lo dirige a 127.0.0.1:9099, el emulador local.

La sesión y la contraseña deben ser sintéticas. Redacten tokens y contraseñas en cualquier captura.
