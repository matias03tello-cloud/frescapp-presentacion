# Guion de presentación — Backend de FrescApp (Hito 2)

**Duración objetivo:** 7 minutos. La presentación interactiva tiene 9 diapositivas.  
**Reparto:** tres bloques consecutivos de diapositivas para reducir los cambios de expositor.

**Nota de ensayo:** antes de presentar, ejecuten la colección en Postman y registren los resultados reales. No afirmen que una operación está comprobada si no la ejecutaron; si algo sigue pendiente, indíquenlo con claridad.

## Integrante 1 — Diapositivas 1–3 · 0:00–2:05

### Diapositiva 1 · Portada · 0:00–0:30

> “En el Hito 1 definimos qué necesitaba FrescApp. En este hito construimos el motor que recibe solicitudes, valida quién las hace, aplica reglas y guarda los datos. Hoy mostraremos el backend que da soporte a inventario y lista de compras.”

### Diapositiva 2 · ¿Qué hace el backend? · 0:30–1:00

> “El backend recibe solicitudes HTTP, verifica la identidad y los datos, aplica las reglas de FrescApp y guarda o consulta la información. Así separamos la pantalla de la lógica y de la persistencia.”

### Diapositiva 3 · Una solicitud recorre cuatro capas · 1:00–2:05

**Selecciona las etapas del diagrama mientras explicas el recorrido.**

> “La solicitud llega al router, que identifica el recurso, el método y el ID. El controlador se ocupa del token, la entrada y la respuesta HTTP. El servicio aplica las reglas del dominio, y el repositorio concentra las consultas a Firestore.”

> “El servidor obtiene el UID desde el ID token verificado; no confía en un UID enviado por el cliente. Así limita cada operación a los datos privados de la cuenta autenticada.”

## Integrante 2 — Diapositivas 4–6 · 2:05–4:45

### Diapositiva 4 · Dos recursos, cuatro operaciones cada uno · 2:05–2:30

> “La API tiene dos recursos: inventario y lista de compras. En ambos podemos crear, leer, actualizar y borrar. Cada uno tiene rutas y datos propios, por eso comprobamos su ciclo CRUD por separado.”

### Diapositiva 5 · Explorador interactivo y demostración Postman · 2:30–4:15

**La diapositiva es un ejemplo didáctico y no envía peticiones. Explica brevemente la operación y cambia a Postman para mostrar las llamadas reales contra Firebase Emulator Suite. Usa una cuenta y datos sintéticos.**

> “La colección se ejecuta localmente contra los emuladores; no usamos APIs externas ni datos de producción. Postman conserva localmente el token que devuelve Auth Emulator.”

> “En inventario ejecutamos POST, GET, PATCH y DELETE. Revisamos 201 al crear, 200 al leer y actualizar, y 204 al borrar. Repetimos el mismo ciclo en lista de compras y confirmamos sus respuestas.”

**Si una operación no se ha ejecutado durante el ensayo, no la presentes como comprobada.** Indica qué quedó pendiente y vuelve a esta evidencia cuando esté lista.

### Diapositiva 6 · El código de estado también comunica · 4:15–4:45

> “Los códigos también describen los errores: 400 indica datos inválidos, 401 un token faltante o no válido y 404 una ruta o un recurso inexistente. Un error devuelto como éxito sería una falla del contrato.”

## Integrante 3 — Diapositivas 7–9 · 4:45–7:00

### Diapositiva 7 · ¿Qué problema resuelve cada opción? · 4:45–5:40

**Usa la comparación interactiva de plataforma y frameworks.**

> “Cloud Functions v2 es la plataforma donde corre el servicio. Express y Fastify son frameworks HTTP que pueden organizar las rutas dentro de esa plataforma. Para dos recursos usamos onRequest y un router propio, con menos dependencias. Aceptamos mantener manualmente el despacho de rutas y los errores.”

> “Si aumentan las rutas comunes o el middleware, podríamos reevaluar Express o Fastify según lo que necesite el proyecto.”

### Diapositiva 8 · Monolito modular para el alcance actual · 5:40–6:40

**Muestra primero la estructura y luego los motivos para mantenerla.**

> “La API es un monolito modular: un servicio publicable contiene los módulos de inventario y lista de compras, separados internamente por capas. Encaja con el equipo y la carga esperada porque ambos recursos comparten autenticación, Firestore y despliegue.”

> “Aceptamos que los dos recursos se publiquen y escalen juntos. Reevaluaríamos la decisión si uno necesitara carga, disponibilidad o despliegue independiente; separar servicios también aumentaría el costo de operación y coordinación.”

### Diapositiva 9 · Cierre · 6:40–7:00

> “El backend combina un contrato REST propio, capas separadas, autenticación y persistencia en Firestore. Elegimos la arquitectura por las necesidades actuales y tenemos claro cuándo volver a evaluarla. Gracias.”

## Resumen del reparto

- **Integrante 1:** diapositivas 1–3; propósito, identidad y capas.
- **Integrante 2:** diapositivas 4–6; recursos, CRUD real en Postman y estados HTTP.
- **Integrante 3:** diapositivas 7–9; plataforma, frameworks, arquitectura y cierre.

## Preparación del equipo

- Ensayar con cronómetro y completar las nueve diapositivas en siete minutos.
- Tener los emuladores iniciados y la colección Postman preparada antes de exponer.
- Usar datos sintéticos y ocultar tokens, contraseñas y datos personales.
- No presentar la animación de la diapositiva 5 como una llamada real; ejecutar Postman para demostrar el CRUD.
- Cada integrante debe poder explicar su parte y cómo se conecta con las demás capas.
