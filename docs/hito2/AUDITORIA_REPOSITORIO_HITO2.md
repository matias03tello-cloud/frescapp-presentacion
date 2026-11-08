# Auditoría de repositorios y backend — Hito 2

**Fecha de revisión:** 8 de noviembre de 2026  
**Repositorios revisados:** [`arq-app-compras`](https://github.com/matias03tello-cloud/arq-app-compras) (código) y [`frescapp-presentacion`](https://github.com/matias03tello-cloud/frescapp-presentacion) (presentaciones y materiales).  
**Estado de GitHub:** los pull requests [#13](https://github.com/matias03tello-cloud/arq-app-compras/pull/13), [#14](https://github.com/matias03tello-cloud/arq-app-compras/pull/14) y [#2](https://github.com/matias03tello-cloud/frescapp-presentacion/pull/2) están fusionados en sus respectivos repositorios.

## Resultado

La API REST del Hito 2 está incorporada al repositorio de código y sus módulos tienen responsabilidades distintas. La revisión inicial detectó respaldos de manifiestos y una diferencia en la cantidad máxima de decimales. El PR #14 retiró los respaldos, los agregó a `.gitignore`, alineó la validación del servidor con la app y añadió pruebas para creación y actualización. La app y la API todavía tienen caminos de acceso a Firestore que se superponen durante la migración.

Este repositorio de presentaciones contiene la demostración interactiva, el guion, el prompt para repetir la prueba y los informes. Para evitar copias que puedan quedar desactualizadas, el informe técnico, el PDF y la colección Postman se enlazan desde el repositorio de código, donde quedaron junto a la implementación.

## Hallazgos

| Prioridad | Hallazgo | Efecto | Estado o acción |
|---|---|---|---|
| Resuelto | Cuatro respaldos de `package.json` y `package-lock.json` estaban versionados; los dos `package.json` eran idénticos y los lockfiles eran copias antiguas sin referencias de ejecución. | Confundían cuál manifiesto debía usar `npm ci` y añadían archivos grandes. | El [PR #14](https://github.com/matias03tello-cloud/arq-app-compras/pull/14) los retiró y agregó exclusiones en `.gitignore`. |
| Media | La app conserva servicios que consultan Firestore directamente, mientras la API REST implementa inventario y lista de compras en `functions/api/`. | Hay dos caminos de acceso al mismo dominio, pero todavía no dos despliegues equivalentes: el cliente no fue migrado a REST. | Es una transición deliberada para evaluar el backend por separado. Mantenerla documentada y migrar pantalla por pantalla antes de retirar el acceso directo. |
| Resuelto | La app y la API aplicaban reglas distintas para decimales de lista de compras. | Una cantidad podía aceptarse por Postman y rechazarse desde la app. | El [PR #14](https://github.com/matias03tello-cloud/arq-app-compras/pull/14) alineó el máximo de tres decimales al crear y actualizar, con tres pruebas dirigidas aprobadas. |
| Media | La suite ahora incluye pruebas dirigidas para la validación de compras, pero no una suite automatizada completa para rutas, autenticación y errores HTTP. | Los códigos y respuestas del controlador todavía pueden cambiar sin una prueba de contrato específica. | Mantener Postman para la demostración y considerar pruebas automatizadas del contrato REST como trabajo pendiente. |
| Alta | El informe de Matías registra un CRUD previo de inventario, pero no adjunta capturas; el CRUD de lista no tiene resultados registrados. El informe asignado a Benjamín sigue sin datos de ejecución. | Los entregables no evidencian todavía los dos recursos y la repetición en otro computador. | Completar ambas tablas con respuestas observadas y guardar capturas redactadas antes de marcar el paso 9 como cerrado. |
| Resuelto | El informe técnico y la colección Postman estaban copiados en ambos repositorios. El PDF ya estaba únicamente en el repositorio de código. | Las instrucciones y la colección podían divergir después de un cambio al backend. | El [PR #2](https://github.com/matias03tello-cloud/frescapp-presentacion/pull/2) retiró las copias y dejó enlaces a la guía, el PDF y la colección canónicos. |

## Organización actual

- **Código y contrato REST:** `arq-app-compras`, incluyendo `functions/api/`, el modelo de datos, el informe técnico, el PDF y la colección Postman.
- **Presentación y evidencia:** `frescapp-presentacion`, incluyendo la página interactiva, el guion, el prompt de repetición y los informes de prueba.
- **Capas del backend:** rutas y controlador atienden HTTP; el servicio aplica reglas; el repositorio concentra Firestore; los validadores no hacen I/O. No se observó que dos módulos de `functions/api/` implementen la misma responsabilidad.
- **APIs externas:** no se incorporan. La demostración usa la API REST propia y Firebase Emulator Suite en localhost.

## Validación ejecutada

- Las tres pruebas dirigidas de la validación de compras pasan.
- La suite completa de Functions en la copia de trabajo compartida dio 31/33: fallaron `CSV roto falla explícitamente` y `Cabecera o filas desplazadas fallan sin generar catálogo`, ambas del importador CSV. Esa copia contiene cambios locales de catálogo que no se incluyeron en el PR #14.
- No se encontró una ejecución de GitHub Actions asociada al commit de fusión del PR #14. Conviene volver a ejecutar la suite en un checkout limpio antes de afirmar que todas las pruebas del repositorio pasan.

## Pendiente para cerrar la revisión

1. Registrar las respuestas y capturas de ambos CRUD, incluido el computador de Benjamín.
2. Considerar pruebas automatizadas de contrato para rutas, autenticación y errores HTTP; las pruebas actuales cubren la validación de compras.
3. Migrar gradualmente la app a REST solo cuando cada pantalla esté integrada y comprobada.

La auditoría es estática: no declara como ejecutados los CRUD que no tienen evidencia en los informes ni afirma que el conjunto del backend haya sido probado de nuevo en esta revisión.

