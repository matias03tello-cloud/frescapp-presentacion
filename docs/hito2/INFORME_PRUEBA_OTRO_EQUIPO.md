# Informe de prueba del backend en otro equipo — Benjamín

## Resumen de resultados

**Resultado:** CRUD de inventario y lista de compras observado en Postman Local contra Firebase Emulator Suite, con estados HTTP esperados y observaciones de reproducibilidad. Las solicitudes se enviaron individualmente; no se ejecutó Postman Runner ni hubo aserciones automáticas.

**Sesión CRUD:** 11 de noviembre de 2026, aproximadamente entre 21:58 y 22:03, hora de Santiago (UTC-03:00).  
**Consolidación documental:** 14 de noviembre de 2026. Versión reorganizada para lectura: 22 de noviembre de 2026.

## 1. Identificación y alcance

- Proyecto: FrescApp — Hito 2.
- Integrante que realizó esta prueba: **Benjamín**.
- Equipo: segundo computador Windows. El hostname y la ruta local se omiten en esta copia publicada.
- Sistema observado: Windows NT 10.0.26300.0; edición no registrada.
- Ubicación/laboratorio y marca/modelo físico: pendientes de registrar.
- Archivo del proyecto: `arq-app-compras-main.zip`, 3.043.984 bytes.
- SHA-256 del archivo: `7322F6A2B7AE58BD1F0C5D204CA89BDF29D7BC60AA06C879B9234BD85998BC6E`.
- Commit exacto probado: pendiente; no se registró un hash de commit.
- Alcance: solicitudes locales con datos sintéticos. No se usó el backend de producción. Este registro describe las pruebas observadas y no constituye una auditoría de seguridad ni una nueva ejecución independiente.

## 2. Herramientas y versiones observadas

| Herramienta | Versión observada | Nota |
|---|---|---|
| Node.js usado para Firebase CLI y los emuladores | 22.23.5 | Se ejecutó el runtime Node 22 descargado para esta prueba; es el runtime requerido por Functions. |
| Node.js global del equipo | 24.19.0 | No fue el runtime utilizado para ejecutar Firebase CLI en esta prueba. |
| npm | Versión no registrada | Se ejecutó `npm ci --prefix functions`; no se ejecutó `npm ci` en la raíz. |
| Java | OpenJDK 21.0.12.1, Temurin | Permitió utilizar Firebase CLI y los emuladores. |
| Firebase CLI | 15.32.1 | Ejecutado con Node.js 22.23.5. |
| Postman Desktop | 12.36.2 durante la prueba | En el cierre documental el lanzador mostró 12.36.4; se conserva la versión histórica de ejecución como 12.36.2. |

## 3. Preparación y configuración

La copia del ZIP se abrió en el segundo equipo. Se instalaron las dependencias de Functions con `npm ci --prefix functions`; no se instalaron las dependencias del cliente Expo desde la raíz.

Se levantaron los emuladores locales para el proyecto `demo-frescapp-hito2`:

- Authentication Emulator: `127.0.0.1:9099`.
- Firestore Emulator: `127.0.0.1:8080`.
- Functions Emulator: `127.0.0.1:5001`.
- URL base comprobada: `http://127.0.0.1:5001/demo-frescapp-hito2/southamerica-west1/api`.

La colección se abrió en Postman en modo **Local**, sin sincronizarla con la nube y sin seleccionar un entorno separado. Se creó una cuenta sintética en Auth Emulator y se utilizaron el token y el UID locales. El script `db/crear-estructura-hito2.cjs` preparó datos sintéticos en Firestore Emulator. No se incluyeron contraseñas ni tokens en este informe.

La colección original del ZIP se conservó. En la copia local de Postman se añadió una solicitud GET de colección de inventario después de contrastar su ruta con el contrato REST. La revisión no inventó una prueba de validación de errores: el ZIP no incluía una solicitud específica para ese caso.

## 4. Resultados del CRUD de inventario

La colección registra estas cinco solicitudes individuales:

| Operación | Petición | Estado esperado | Estado observado | Resultado |
|---|---|---:|---:|---|
| Crear | `POST /v1/inventario` | 201 | 201 Created | Observado |
| Leer colección | `GET /v1/inventario?limit=50` | 200 | 200 OK | Observado |
| Leer registro | `GET /v1/inventario/{id}` | 200 | 200 OK | Observado |
| Actualizar | `PATCH /v1/inventario/{id}` | 200 | 200 OK | Observado |
| Borrar | `DELETE /v1/inventario/{id}` | 204 | 204 No Content | Observado |

La creación registrada usó un producto sintético de inventario. La actualización cambió cantidad y ubicación y la respuesta conservó el mismo identificador del registro.

**Incidencia de inicio:** el primer POST se envió antes de que la función `api` estuviera cargada y respondió 404. Tras recargar el observador de Functions, la ruta quedó disponible y el POST respondió 201. Se conservan ambas capturas para mostrar el fallo inicial y la respuesta posterior.

## 5. Resultados del CRUD de lista de compras

| Operación | Petición | Estado esperado | Estado observado | Resultado |
|---|---|---:|---:|---|
| Crear | `POST /v1/lista-compras` | 201 | 201 Created | Observado |
| Leer colección | `GET /v1/lista-compras?limit=50` | 200 | 200 OK | Observado |
| Leer registro | `GET /v1/lista-compras/{id}` | 200 | 200 OK | Observado |
| Actualizar | `PATCH /v1/lista-compras/{id}` | 200 | 200 OK | Observado |
| Borrar | `DELETE /v1/lista-compras/{id}` | 204 | 204 No Content | Observado |

La actualización de la lista de compras cambió cantidad y estado de compra; la respuesta conservó el identificador y nombre del registro.

## 6. Cómo se registraron los resultados

- El historial de Postman muestra los diez envíos exitosos de ambos recursos, además del alta de la cuenta sintética y del POST inicial que falló con 404.
- Cada solicitud se envió y revisó individualmente. **No se ejecutó el Runner** para esta colección y no se registraron aserciones automatizadas.
- Postman conservó los códigos, tiempos y tamaños de respuesta en el historial; según la configuración observada, los cuerpos no quedan almacenados en dicho historial.
- Las capturas de las respuestas originales y los registros de Firebase se conservaron en el paquete de evidencia del equipo. El PDF fuente incluye imágenes de la creación de inventario, actualización de lista de compras y estado de los emuladores.
- La captura del estado de emuladores corresponde a una revisión del 14 de noviembre; no se presenta como una captura tomada durante la sesión CRUD del día 11.

## 7. Observaciones y límites

- No se ejecutó un GET posterior a cada DELETE. Por ello, el informe confirma la respuesta 204 observada, pero no afirma que se haya verificado después la ausencia del documento.
- No se ejecutó una petición inválida de validación; la colección del ZIP no incluía ese caso y no se añadió una prueba inventada.
- La instalación completa desde cero no quedó probada: se instaló Functions, pero no se ejecutó `npm ci` desde la raíz.
- El primer arranque de los emuladores terminó con un timeout del hub. El segundo intento cargó la función `api`; no se atribuye una causa definitiva al primer timeout.
- Se observaron advertencias de `ENFORCE_APP_CHECK` y una función programada que dependía de Pub/Sub; no fueron objeto de estas pruebas CRUD.
- No se ejecutó `npm audit fix` ni se realizó una auditoría de vulnerabilidades o de seguridad.
- Quedan por registrar la ubicación/laboratorio, el modelo físico del equipo, la edición de Windows, el hash del commit y capturas originales de las salidas de versión.

## 8. Conclusión

En el segundo equipo, las solicitudes individuales de inventario y lista de compras recibieron los códigos HTTP esperados en Firebase Emulator Suite: creación 201, lecturas y actualización 200, y borrado 204. El informe queda **aprobado con observaciones para las operaciones CRUD ejecutadas**. No acredita una ejecución del Runner, una lectura posterior al borrado, una prueba de validación de error ni una instalación completa de todas las dependencias desde cero.
