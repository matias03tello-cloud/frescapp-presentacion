# Figuras de evidencia para el informe del Hito 2

Las figuras 1, 2, 3 y 7 son materiales visuales preparados a partir del backend actual. Las figuras 4, 5, 6 y 8 deben capturarse durante una ejecución real; no se deben rellenar con capturas simuladas.

## Figuras ya preparadas

| Número | Archivo | Uso |
|---:|---|---|
| 1 | `figuras/figura-01-arquitectura.svg` | Recorrido desde el cliente hasta Firestore y verificación de identidad. |
| 2 | `figuras/figura-02-estructura-backend.svg` | Árbol real de `functions/` y responsabilidades por capa. Es una visualización del árbol, no una captura del Explorador de archivos. |
| 3 | `figuras/figura-03-modelo-firestore.svg` | Colecciones privadas por usuario y catálogo compartido. |
| 7 | `figuras/figura-07-seguridad.svg` | Exclusiones de credenciales, archivos de ejemplo y control del ID token. Es un esquema basado en archivos, no una captura literal del editor. |

Los archivos son SVG vectoriales y se pueden insertar en Word como imágenes. Los esquemas fueron contrastados con `functions/api/README.md`, `db/MODELO_HITO2.md`, `.gitignore`, `.env.example`, `functions/.env.example` y `functions/api/controller.js`.

## Cómo capturar las figuras pendientes

Antes de capturar, usa solo datos sintéticos y oculta `Authorization`, `idToken`, contraseñas, correos personales y cualquier clave. El ensayo de FrescApp se hace contra Firebase Emulator Suite con el proyecto `demo-frescapp-hito2`, no contra producción.

### Figura 4 · Registro persistido en Firestore Emulator

1. Con los emuladores activos, crea un registro de inventario usando la colección Postman.
2. Abre `http://127.0.0.1:4000/firestore`.
3. Busca `usuarios/{uid}/inventario/{id}` y muestra el documento y sus campos.
4. Captura la ventana con el nombre del emulador visible. No uses la consola de producción para esta prueba local.

### Figura 5 · POST de inventario con respuesta 201

1. En Postman, abre `1. POST inventario (crear)`.
2. Confirma que la URL apunta al emulador local y que el cuerpo contiene datos sintéticos válidos.
3. Envía la petición y captura método/ruta, el cuerpo JSON y el estado `201 Created`.
4. Redacta la cabecera Authorization antes de adjuntar la imagen.

### Figura 6 · Entrada inválida y error HTTP

1. Usa una petición autenticada del recurso de inventario o de lista de compras.
2. Para esta ejecución, quita temporalmente un campo obligatorio o coloca un valor inválido en el cuerpo JSON.
3. Envía la petición y captura el estado `400` y el error JSON devuelto por la API.
4. No guardes el cuerpo inválido como ejemplo de éxito; restablece después el cuerpo correcto.

### Figura 8 · Resultados reales de las pruebas

1. Ejecuta en Postman las cuatro operaciones CRUD de inventario y las cuatro de lista de compras.
2. Verifica los estados de creación, lectura, actualización y borrado en cada recurso.
3. Captura el resumen del Runner y, si no caben los ocho resultados legiblemente, usa dos capturas: una por recurso.
4. Registra en el informe la fecha, el equipo, las versiones de herramientas y cualquier diferencia del ensayo.

Las figuras 5 y 8 pueden compartir evidencia si una captura del Runner muestra claramente las peticiones y estados. No declares aprobada una operación que no se haya ejecutado.

