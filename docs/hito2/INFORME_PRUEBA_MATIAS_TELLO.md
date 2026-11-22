# Informe de prueba del backend en el equipo de Matías Tello

## 1. Identificación

- Proyecto: FrescApp — Hito 2.
- Integrante: Matías Tello.
- Actualización documental: 22 de noviembre de 2026. Las pruebas aquí descritas se realizaron los días 11 y 13 de noviembre de 2026.
- Equipo: computador principal del proyecto.
- Sistema observado: Windows, versión 10.0.26200.0; edición no registrada.
- Versión del proyecto: copia local utilizada durante las pruebas. No se guardó el hash del commit, por lo que estos resultados no se atribuyen a un commit específico de `main`.
- Alcance: peticiones locales con datos sintéticos contra Firebase Emulator Suite. No se usó el backend de producción.

Este informe consolida las capturas originales disponibles. No representa una nueva ejecución realizada al actualizar el documento.

## 2. Herramientas observadas

| Herramienta | Versión observada | Resultado y limitación |
|---|---|---|
| Node.js global | `v24.19.0` | Los emuladores y las peticiones funcionaron, pero Functions declara Node.js 22. La repetición con Node 22 queda pendiente para verificar el runtime requerido. |
| npm | `11.17.0` | Versión observada. No se reinstalaron las dependencias en esta sesión. |
| Java | `21.0.13` | Confirmado; permitió iniciar los emuladores. |
| Firebase CLI | `15.32.1` | Usado para iniciar los emuladores locales. |
| Postman Desktop | `12.36.2` | Usado en modo Local; la colección no se sincronizó con la nube. |

## 3. Preparación del entorno

- Proyecto local de Firebase: `demo-frescapp-hito2`.
- Emuladores utilizados: Authentication, Firestore y Functions.
- Auth Emulator: `127.0.0.1:9099`.
- API local: `http://127.0.0.1:5001/demo-frescapp-hito2/southamerica-west1/api`.
- Se creó una cuenta sintética en Auth Emulator y Postman guardó el token como variable local. No se incluyen contraseñas ni tokens en este informe.
- Para preparar datos sintéticos se usó el script `db/crear-estructura-hito2.cjs` contra Firestore Emulator.
- La colección está publicada en el [repositorio del backend](https://github.com/matias03tello-cloud/arq-app-compras/blob/main/docs/hito2/FrescApp-Hito2.postman_collection.json).

## 4. CRUD de inventario

Ejecución local observada el **11 de noviembre de 2026, 16:16:38**. Postman Runner envió una iteración con las cuatro solicitudes. La captura muestra los estados HTTP recibidos; el panel indica `All tests 0` y `No tests found`, por lo que esta ejecución no tuvo aserciones automatizadas de Postman.

| Operación | Petición | Estado esperado | Estado observado |
|---|---|---:|---:|
| Crear | `POST /v1/inventario` | 201 | 201 |
| Leer registro | `GET /v1/inventario/{id}` | 200 | 200 |
| Actualizar | `PATCH /v1/inventario/{id}` | 200 | 200 |
| Borrar | `DELETE /v1/inventario/{id}` | 204 | 204 |

[Captura del CRUD de inventario](evidencias/capturas/paso-04-inventario-crud-runner-20261111.jpg).

## 5. CRUD de lista de compras

Ejecución local observada el **11 de noviembre de 2026, 17:49:28**. Postman Runner envió una iteración con cinco solicitudes, incluyendo lectura de la colección y del registro. La captura muestra las respuestas HTTP; como en inventario, el Runner indica cero aserciones automatizadas.

| Operación | Petición | Estado esperado | Estado observado |
|---|---|---:|---:|
| Crear | `POST /v1/lista-compras` | 201 | 201 |
| Leer colección | `GET /v1/lista-compras?limit=50` | 200 | 200 |
| Leer registro | `GET /v1/lista-compras/{id}` | 200 | 200 |
| Actualizar | `PATCH /v1/lista-compras/{id}` | 200 | 200 |
| Borrar | `DELETE /v1/lista-compras/{id}` | 204 | 204 |

[Captura del CRUD de lista de compras](evidencias/capturas/paso-06-lista-compras-crud-runner-20261111.jpg).

## 6. Validación de entrada y respuesta de error

El **13 de noviembre de 2026** se envió `POST /v1/lista-compras` al emulador con `cantidad: 0`. Postman mostró `400 Bad Request` y el cuerpo:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Cantidad debe ser mayor que 0 y menor o igual que 999."
  }
}
```

[Captura de la respuesta 400](evidencias/capturas/paso-06-lista-compras-error-validacion-400-postman.jpg).

## 7. Alcance de la evidencia y pendientes

- Las capturas prueban que las solicitudes mostradas recibieron los estados indicados desde la API local.
- No se ejecutó un `GET` posterior al `DELETE`; por tanto, no se afirma que se haya verificado la ausencia del registro después de borrarlo.
- El Runner no tenía scripts de prueba: Postman muestra cero aserciones. Los estados se revisaron en las respuestas visibles.
- La ejecución local se hizo con Node.js global 24.19.0, mientras que el proyecto declara Node.js 22. Repetir el arranque y el CRUD con Node.js 22 sigue pendiente para confirmar la versión requerida.
- No se registró el hash exacto del commit utilizado durante estas pruebas.
- La prueba en otro equipo se documenta por separado en el informe de Benjamín; no forma parte de esta ejecución individual.

## 8. Conclusión

En el equipo principal se observaron respuestas correctas para las operaciones CRUD capturadas de inventario y lista de compras, además de una validación de cantidad que respondió con `400` y `VALIDATION_ERROR`. Esta evidencia corresponde a Firebase Emulator Suite y datos sintéticos. Las limitaciones de runtime, ausencia de aserciones automáticas y falta de un GET posterior al borrado quedan declaradas para no atribuir a las capturas más de lo que demuestran.
