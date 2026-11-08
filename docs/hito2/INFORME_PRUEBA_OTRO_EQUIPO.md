# Informe de prueba del backend en otro equipo

## 1. Identificación

- Proyecto: FrescApp — Hito 2
- Integrante que ejecuta la prueba:
- Fecha y hora:
- Ubicación/laboratorio:
- Equipo (marca/modelo o nombre):
- Sistema operativo y versión:
- Commit o versión del proyecto:

## 2. Herramientas

| Herramienta | Versión instalada | Evidencia |
|---|---|---|
| Node.js (se requiere 22) | | Captura de `node --version` |
| Java (se requiere 21 para Firebase CLI) | | Captura de `java -version` |
| Firebase CLI | | Captura de `firebase --version` |
| Postman | | Captura de versión/ventana About |

## 3. Preparación

Registrar si se completó cada paso. No pegar contraseñas, tokens ni claves privadas en este informe.

- [ ] Abrimos la carpeta FrescApp desde el equipo de prueba.
- [ ] Instalamos dependencias raíz con `npm ci`.
- [ ] Instalamos dependencias de Functions con `npm ci --prefix functions`.
- [ ] Iniciamos Auth, Firestore y Functions Emulator con `npx firebase emulators:start --only auth,firestore,functions --project demo-frescapp-hito2`.
- [ ] Importamos localmente `FrescApp-Hito2.postman_collection.json` en Postman.
- [ ] Creamos la cuenta sintética del emulador y dejamos que Postman guarde el token local.
- [ ] Si se ejecutó el script de semilla, se verificó que el proyecto fuera `demo-*` y apuntara al emulador local.

Notas de preparación / errores encontrados:

## 4. Resultados del CRUD de inventario

| Operación | Petición | Estado esperado | Estado observado | Resultado |
|---|---|---:|---:|---|
| Crear | `POST /v1/inventario` | 201 | | Pendiente |
| Leer | `GET /v1/inventario/{id}` | 200 | | Pendiente |
| Actualizar | `PATCH /v1/inventario/{id}` | 200 | | Pendiente |
| Borrar | `DELETE /v1/inventario/{id}` | 204 | | Pendiente |

Después de borrar, opcionalmente repetir el GET para verificar que responde `404 NOT_FOUND`.

## 5. Resultados del CRUD de lista de compras

| Operación | Petición | Estado esperado | Estado observado | Resultado |
|---|---|---:|---:|---|
| Crear | `POST /v1/lista-compras` | 201 | | Pendiente |
| Leer | `GET /v1/lista-compras/{id}` | 200 | | Pendiente |
| Actualizar | `PATCH /v1/lista-compras/{id}` | 200 | | Pendiente |
| Borrar | `DELETE /v1/lista-compras/{id}` | 204 | | Pendiente |

Después de borrar, opcionalmente repetir el GET para verificar que responde `404 NOT_FOUND`.

## 6. Evidencias adjuntas

Usar capturas legibles que permitan ver nombre de la petición, método/ruta, estado HTTP y respuesta. Se puede adjuntar una captura por operación o una captura del historial de Postman más capturas de los casos que no se distingan en él.

| Archivo | Qué demuestra |
|---|---|
| `01-versiones-herramientas.png` | Versiones del equipo distinto |
| `02-emuladores-iniciados.png` | Emuladores locales en ejecución |
| `03-inventario-post-get.png` | Alta y lectura de inventario |
| `04-inventario-patch-delete.png` | Actualización y borrado de inventario |
| `05-lista-post-get.png` | Alta y lectura de lista de compras |
| `06-lista-patch-delete.png` | Actualización y borrado de lista de compras |
| `07-prueba-luego-de-borrar.png` | Opcional: `404` tras eliminar |

**Privacidad de las capturas:** antes de compartirlas, ocultar el valor de `Authorization`, `idToken`, contraseñas, correo personal, claves o datos identificables. Se pueden mostrar el status HTTP y datos sintéticos.

## 7. Conclusión

- Resultado general: Pendiente / Aprobado / Aprobado con observaciones / No aprobado
- ¿Se pudo levantar siguiendo las instrucciones?:
- ¿Funcionaron ambos recursos?:
- Diferencias respecto al computador principal:
- Errores que se deben corregir:
- Responsable y fecha de cierre:

