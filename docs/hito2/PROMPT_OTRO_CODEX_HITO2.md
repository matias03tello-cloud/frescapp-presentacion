# Instrucción para repetir el Hito 2 en otra computadora con Codex

Copia este texto en Codex después de abrir la carpeta FrescApp sincronizada en el otro computador. Si la ubicación de OneDrive cambia, selecciona manualmente esa carpeta en Codex.

```text
Necesito reproducir la demostración local del backend de FrescApp, Hito 2, en este computador y documentarla en el informe de prueba.

Usa la carpeta abierta como raíz del proyecto. No publiques ni sincronices la colección con la nube de Postman. No uses servicios reales ni APIs externas: toda petición debe ir a Firebase Emulator Suite en localhost. No despliegues Functions.

Lee primero docs/hito2/BACKEND_HITO2.md, docs/hito2/INFORME_PRUEBA_OTRO_EQUIPO.md y la colección docs/hito2/FrescApp-Hito2.postman_collection.json. Comprueba que el árbol corresponde a FrescApp y revisa el package.json y firebase.json.

1. Registra en el informe fecha, sistema operativo, versiones de Node.js, Java, Firebase CLI y Postman. El proyecto documenta Node 22 y Java 21.
2. Guíame para ejecutar npm ci y npm ci --prefix functions solo si las dependencias no están instaladas.
3. Inicia localmente Auth, Firestore y Functions Emulator para el proyecto demo-frescapp-hito2. Comprueba que la URL base sea http://127.0.0.1:5001/demo-frescapp-hito2/southamerica-west1/api y que Auth Emulator use el puerto 9099.
4. Indícame cómo importar la colección JSON como archivo local en Postman; no la importes a un workspace sincronizado. Asigna a la variable local password una contraseña sintética solo para el emulador.
5. Ejecuta primero “0. Crear cuenta local y guardar token”. Después prepara solo datos sintéticos en el emulador si hace falta. El script db/crear-estructura-hito2.cjs solo debe ejecutarse con FIRESTORE_EMULATOR_HOST=127.0.0.1:8080 y un proyecto demo-*; nunca apuntes a producción.
6. Prueba en orden POST, GET por ID, PATCH y DELETE para inventario; confirma 201, 200, 200 y 204. Luego completa las mismas cuatro operaciones para lista de compras. Los IDs se guardan en variables de la colección.
7. Si falla una petición, conserva método, URL local, status y mensaje del error; no muestres ni copies el token, la contraseña ni el encabezado Authorization. No cambies el código durante la prueba sin registrar el cambio.
8. Ayúdame a completar docs/hito2/INFORME_PRUEBA_OTRO_EQUIPO.md con los resultados reales y una lista de capturas. No declares una operación exitosa sin ver su respuesta en Postman.

Al final, resume qué funcionó, qué falló y qué evidencias guardar. Deja los emuladores en ejecución hasta que confirme que terminé de sacar las capturas; luego ayúdame a apagarlos de forma normal.
```

## Colección Postman compartible

La colección usa solo direcciones del emulador local (`127.0.0.1`), cuenta sintética y variables vacías para secretos. En otra computadora debe ejecutarse con Firebase Emulator Suite iniciada; el archivo no se conecta a un backend público.

Enlace directo al JSON para adjuntarlo al Codex o descargarlo e importarlo localmente en Postman:  
https://raw.githubusercontent.com/matias03tello-cloud/frescapp-presentacion/main/docs/hito2/FrescApp-Hito2.postman_collection.json

