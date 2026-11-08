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
| Media | En `arq-app-compras` están versionados `package.json.antes-audit`, `package.json.respaldo-raiz`, `package-lock.json.antes-audit` y `package-lock.json.respaldo-raiz`. Los dos respaldos de `package.json` son idénticos entre sí; los lockfiles de respaldo son distintos del lockfile activo y entre sí. No se encontraron referencias de ejecución a esos nombres. | Confunden cuál manifiesto debe usar `npm ci` y añaden archivos grandes que no son necesarios para instalar. | Conviene retirarlos en una revisión del repositorio de código. El historial de Git conserva las versiones anteriores. |
| Media | La app conserva servicios que consultan Firestore directamente, mientras la API REST implementa inventario y lista de compras en `functions/api/`. | Hay dos caminos de acceso al mismo dominio, pero todavía no dos despliegues equivalentes: el cliente no fue migrado a REST. | Es una transición deliberada para evaluar el backend por separado. Mantenerla documentada y migrar pantalla por pantalla antes de retirar el acceso directo. |
| Media | `services/comprasModelo.ts` limita cantidades a tres decimales. El validador REST de lista de compras limita el rango y exige enteros para `unidad`, pero no aplica el mismo máximo de tres decimales. | Una cantidad podría aceptarse por Postman y rechazarse desde la app. | Alinear la regla del backend y conservar su validación independiente; nunca confiar solo en el cliente. |
| Media | La prueba REST está documentada mediante Postman; no se encontró una suite automatizada dedicada al contrato de rutas, autenticación y errores HTTP. | Un cambio puede alterar códigos o mensajes sin que una prueba automática lo detecte. | Mantener Postman para la demostración y considerar pruebas de contrato automatizadas como trabajo pendiente. |
| Alta | El informe de Matías registra un CRUD previo de inventario, pero no adjunta capturas; el CRUD de lista no tiene resultados registrados. El informe asignado a Benjamín sigue sin datos de ejecución. | Los entregables no evidencian todavía los dos recursos y la repetición en otro computador. | Completar ambas tablas con respuestas observadas y guardar capturas redactadas antes de marcar el paso 9 como cerrado. |
| Baja | El informe técnico y la colección Postman estaban copiados en ambos repositorios. El PDF ya estaba únicamente en el repositorio de código. | Las instrucciones y la colección podían divergir después de un cambio al backend. | Este cambio retira las dos copias y enlaza la guía, el PDF y la colección desde su ubicación canónica en el repositorio de código. |

## Organización actual

- **Código y contrato REST:** `arq-app-compras`, incluyendo `functions/api/`, el modelo de datos, el informe técnico, el PDF y la colección Postman.
- **Presentación y evidencia:** `frescapp-presentacion`, incluyendo la página interactiva, el guion, el prompt de repetición y los informes de prueba.
- **Capas del backend:** rutas y controlador atienden HTTP; el servicio aplica reglas; el repositorio concentra Firestore; los validadores no hacen I/O. No se observó que dos módulos de `functions/api/` implementen la misma responsabilidad.
- **APIs externas:** no se incorporan. La demostración usa la API REST propia y Firebase Emulator Suite en localhost.

## Pendiente para cerrar la revisión

1. Retirar los cuatro respaldos de manifiestos del repositorio de código en un cambio revisado.
2. Alinear el máximo de tres decimales para la lista de compras entre app y API.
3. Registrar las respuestas y capturas de ambos CRUD, incluido el computador de Benjamín.
4. Considerar pruebas automatizadas de contrato para rutas, autenticación, validación y errores.
5. Migrar gradualmente la app a REST solo cuando cada pantalla esté integrada y comprobada.

La auditoría es estática: no declara como ejecutados los CRUD que no tienen evidencia en los informes ni afirma que el conjunto del backend haya sido probado de nuevo en esta revisión.

