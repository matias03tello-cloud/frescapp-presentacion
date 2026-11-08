# Auditoría de repositorios y backend — Hito 2

**Fecha de revisión:** 8 de noviembre de 2026  
**Repositorios revisados:** [`arq-app-compras`](https://github.com/matias03tello-cloud/arq-app-compras) (código) y [`frescapp-presentacion`](https://github.com/matias03tello-cloud/frescapp-presentacion) (presentaciones y materiales).  
**Estado del backend:** el pull request [#13](https://github.com/matias03tello-cloud/arq-app-compras/pull/13) está fusionado en `main`.

## Resultado

La API REST del Hito 2 ya está incorporada al repositorio de código y sus módulos tienen responsabilidades distintas. Esta revisión encontró archivos de respaldo de manifiestos que sobran, una regla de cantidad que difiere entre la app y la API, y rutas de acceso a Firestore que se superponen mientras la app todavía no migra al backend REST.

Este repositorio de presentaciones contiene la demostración interactiva, el guion, el prompt para repetir la prueba y los informes. Para evitar copias que puedan quedar desactualizadas, el informe técnico, el PDF y la colección Postman se enlazan desde el repositorio de código, donde quedaron junto a la implementación.

## Hallazgos

| Prioridad | Hallazgo | Efecto | Estado o acción |
|---|---|---|---|
| Media | En `arq-app-compras` estaban versionados cuatro respaldos de manifiestos; los dos `package.json` son idénticos y los lockfiles son copias antiguas sin referencias de ejecución. | Confunden cuál manifiesto debe usar `npm ci` y añaden archivos grandes que no son necesarios para instalar. | El [PR #14](https://github.com/matias03tello-cloud/arq-app-compras/pull/14) los elimina y añade exclusiones; pendiente de revisión y fusión. |
| Media | La app conserva servicios que consultan Firestore directamente, mientras la API REST implementa inventario y lista de compras en `functions/api/`. | Hay dos caminos de acceso al mismo dominio, pero todavía no dos despliegues equivalentes: el cliente no fue migrado a REST. | Es una transición deliberada para evaluar el backend por separado. Mantenerla documentada y migrar pantalla por pantalla antes de retirar el acceso directo. |
| Media | La app y la API aplicaban reglas distintas para decimales de lista de compras. | Una cantidad podía aceptarse por Postman y rechazarse desde la app. | El [PR #14](https://github.com/matias03tello-cloud/arq-app-compras/pull/14) alinea el máximo de tres decimales al crear y actualizar, con tres pruebas dirigidas aprobadas; pendiente de revisión y fusión. |
| Media | La suite ahora incluye pruebas dirigidas para la validación de compras, pero no una suite automatizada completa para rutas, autenticación y errores HTTP. | Los códigos y respuestas del controlador todavía pueden cambiar sin una prueba de contrato específica. | Mantener Postman para la demostración y considerar pruebas automatizadas del contrato REST como trabajo pendiente. |
| Alta | El informe de Matías registra un CRUD previo de inventario, pero no adjunta capturas; el CRUD de lista no tiene resultados registrados. El informe asignado a Benjamín sigue sin datos de ejecución. | Los entregables no evidencian todavía los dos recursos y la repetición en otro computador. | Completar ambas tablas con respuestas observadas y guardar capturas redactadas antes de marcar el paso 9 como cerrado. |
| Baja | El informe técnico y la colección Postman estaban copiados en ambos repositorios. El PDF ya estaba únicamente en el repositorio de código. | Las instrucciones y la colección podían divergir después de un cambio al backend. | Este cambio retira las dos copias y enlaza la guía, el PDF y la colección desde su ubicación canónica en el repositorio de código. |

## Organización actual

- **Código y contrato REST:** `arq-app-compras`, incluyendo `functions/api/`, el modelo de datos, el informe técnico, el PDF y la colección Postman.
- **Presentación y evidencia:** `frescapp-presentacion`, incluyendo la página interactiva, el guion, el prompt de repetición y los informes de prueba.
- **Capas del backend:** rutas y controlador atienden HTTP; el servicio aplica reglas; el repositorio concentra Firestore; los validadores no hacen I/O. No se observó que dos módulos de `functions/api/` implementen la misma responsabilidad.
- **APIs externas:** no se incorporan. La demostración usa la API REST propia y Firebase Emulator Suite en localhost.

## Pendiente para cerrar la revisión

1. Revisar y fusionar el PR #14 del repositorio de código para retirar respaldos y alinear la precisión decimal.
2. Registrar las respuestas y capturas de ambos CRUD, incluido el computador de Benjamín.
3. Considerar pruebas automatizadas de contrato para rutas, autenticación y errores HTTP.
4. Migrar gradualmente la app a REST solo cuando cada pantalla esté integrada y comprobada.

La auditoría es estática: no declara como ejecutados los CRUD que no tienen evidencia en los informes ni afirma que el conjunto del backend haya sido probado de nuevo en esta revisión.

