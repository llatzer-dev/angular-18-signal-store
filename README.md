
# Optimización del Manejo de Estados en Aplicaciones Frontend

## El uso del Store como Single Source of Truth (SSOT)

En el desarrollo de aplicaciones frontend, uno de los patrones más comunes es la interacción entre el cliente (frontend) y el servidor (backend). Generalmente, el flujo sigue esta estructura:

1. El frontend solicita todos los datos al backend. Por ejemplo, una lista de personajes.
2. El usuario edita un personaje, lo que genera una petición de actualización al backend.
3. Después de la actualización, el frontend vuelve a solicitar todos los personajes para asegurarse de que la tabla refleje los cambios.

Este ciclo se repite constantemente: `frontend → dame todo → update → backend → dame todo → frontend`.

Aunque este enfoque es funcional, plantea una pregunta clave: **¿Es necesario volver a pedir toda la información si ya sabemos qué campo se actualizó?** La respuesta es **NO**, y aquí es donde entra en juego el uso de un store en el frontend, lo cual permite optimizar este flujo.

## La Optimización: Evitar Peticiones Redundantes

Imagina que, en lugar de volver a pedir todos los datos al backend, simplemente actualizamos lo que ya sabemos en el frontend. Esto es especialmente útil en situaciones donde los datos no son compartidos entre múltiples usuarios o cuentas. Para estos casos, proponemos el siguiente flujo optimizado:

### Nuevo Flujo:

1. Frontend pide todos los datos (`dame todo`).
2. Los datos se guardan en un store en el frontend.
3. Se realiza una actualización (`update`).
4. Si la actualización es exitosa, se actualiza directamente el store sin necesidad de pedir nuevamente todos los datos al backend.

### Resumen del Nuevo Flujo:

`frontend → dame todo → guardar en el store → update → si va bien → actualizar el store`

## ¿Qué es un Store?

El concepto de **Single Source of Truth (SSOT)** es fundamental en este enfoque. Un store es una representación local, en el frontend, de la base de datos del backend. Contiene información siempre actualizada y confiable, lo que reduce la necesidad de solicitudes redundantes al servidor.

Este patrón se puede implementar con diferentes tecnologías como Zustand, RxJS, Redux, o cualquier manejador de estado global. En nuestro caso, usaremos **NGRX SignalStore** para manejar el estado en Angular.

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 18.1.0.

### Instalar dependencias

Run `npm i`

### Levantar entorno de desarrollo

Run `npm run start` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

### Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.
