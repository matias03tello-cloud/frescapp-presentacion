# Informe de prueba del backend en el equipo de Matías Tello

## 1. Identificación

- Proyecto: FrescApp — Hito 2
- Integrante que presenta este registro: **Matías Tello**
- Fecha de consolidación del informe: **8 de noviembre de 2026**
- Equipo: computador principal del proyecto
- Sistema observado: Windows, versión `10.0.26200.0` (edición no registrada)
- Commit o versión del proyecto: rama local `review-main`; no se registró un hash de commit para esta prueba
- Integrante a cargo del segundo equipo: **Benjamín** (su informe se completa por separado)

## 2. Herramientas observadas

| Herramienta | Versión / estado observado | Requisito documentado | Resultado |
|---|---|---|---|
| Node.js | `v24.19.0` | Node.js 22 | No coincide; preparar Node 22 para la prueba reproducible |
| npm | `11.17.0` | Asociado al Node 22 del proyecto | Versión observada; no se volvió a instalar dependencias en esta sesión |
| Java | Versión no confirmada; no se verificó una instalación de Java 21 | Java 21 | Pendiente de confirmar/instalar antes de iniciar los emuladores |
| Firebase CLI | `15.32.1` | Firebase CLI disponible | Mostró un error de permiso de su comprobación de actualizaciones; versión visible `15.32.1` |
| Postman | Instalado; versión no registrada y aplicación cerrada al momento de esta revisión | Postman | Pendiente capturar la versión |

## 3. Preparación del entorno

- [x] Se identificó el proyecto FrescApp y su configuración local de Firebase Emulator Suite.
- [x] La colección Postman del Hito 2 está disponible en `docs/hito2/FrescApp-Hito2.postman_collection.json`.
- [ ] Verificar Node.js 22, que es la versión declarada por Functions.
- [ ] Confirmar/instalar Java 21 y registrar `java -version`.
- [ ] Iniciar Auth, Firestore y Functions Emulator para `demo-frescapp-hito2`.
- [ ] Importar la colección como archivo local en Postman, sin sincronizarla con la nube.
- [ ] Crear/iniciar la cuenta sintética del Auth Emulator y comprobar que se guarda el token localmente.

**Estado al consolidar este informe:** los puertos locales `5001`, `8080` y `9099` no estaban escuchando; por ello no se ejecutó un nuevo ciclo CRUD en esta sesión. No se usó un backend de producción.

## 4. Resultados del CRUD de inventario

La conversación de pruebas anterior registró un ciclo CRUD exitoso en Postman para inventario. La fecha exacta y las capturas de esa ejecución no quedaron registradas en este informe.

| Operación | Petición | Estado esperado | Estado registrado | Resultado |
|---|---|---:|---:|---|
| Crear | `POST /v1/inventario` | 201 | 201 | Aprobado — ejecución local previa |
| Leer | `GET /v1/inventario/{id}` | 200 | 200 | Aprobado — ejecución local previa |
| Actualizar | `PATCH /v1/inventario/{id}` | 200 | 200 | Aprobado — ejecución local previa |
| Borrar | `DELETE /v1/inventario/{id}` | 204 | 204 | Aprobado — ejecución local previa |

## 5. Resultados del CRUD de lista de compras

La colección contiene las solicitudes para el ciclo completo de lista de compras, pero no quedó un resultado de ejecución observado que pueda registrar aquí.

| Operación | Petición | Estado esperado | Estado registrado | Resultado |
|---|---|---:|---:|---|
| Crear | `POST /v1/lista-compras` | 201 | — | Pendiente de ejecutar |
| Leer | `GET /v1/lista-compras/{id}` | 200 | — | Pendiente de ejecutar |
| Actualizar | `PATCH /v1/lista-compras/{id}` | 200 | — | Pendiente de ejecutar |
| Borrar | `DELETE /v1/lista-compras/{id}` | 204 | — | Pendiente de ejecutar |

## 6. Evidencias

| Archivo | Estado |
|---|---|
| `01-versiones-herramientas.png` | Pendiente de guardar |
| `02-emuladores-iniciados.png` | Pendiente de guardar |
| `03-inventario-post-get.png` | Pendiente de adjuntar desde la ejecución previa |
| `04-inventario-patch-delete.png` | Pendiente de adjuntar desde la ejecución previa |
| `05-lista-post-get.png` | Pendiente de generar |
| `06-lista-patch-delete.png` | Pendiente de generar |

Antes de compartir capturas, ocultar el token `Authorization`, `idToken`, contraseñas, correos personales y cualquier clave. Usar solo datos sintéticos.

## 7. Conclusión

- Resultado general actual: **Parcial**.
- Inventario: CRUD registrado como exitoso en una ejecución local anterior.
- Lista de compras: CRUD todavía sin resultados registrados en este informe.
- Prueba actual en otro computador: pendiente; la realizará Benjamín y quedará en su informe separado.
- Para cerrar este informe: preparar Node 22 y Java 21, ejecutar ambos CRUD en Postman contra los emuladores y adjuntar capturas de las respuestas observadas.
