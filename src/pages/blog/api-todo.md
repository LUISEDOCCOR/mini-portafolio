---
layout: ../../layouts/Blog.astro
title: Utiliza esta API gratuita para crear tu app de tareas
desc: Esta API permite la creación de una aplicación de gestión de tareas, donde los usuarios pueden registrarse, autenticarse y realizar operaciones CRUD sobre las tareas.
date: 25/09/2024
image_path: /og.webp
---

Esta API de gestión de tareas permite a los usuarios registrarse,
autenticarse mediante `JWT` y realizar operaciones `CRUD`, incluyendo
la capacidad de obtener tareas filtradas por estado (como "completadas" o "pendientes").


Esta API de gestión de tareas está hecha en `Go`, lo que la hace rápida y eficiente.
Gracias a Go, la API puede manejar `muchas solicitudes al mismo tiempo` sin problemas

## La URL base es la siguiente 
```bash
https://api.luiseduardocortes.xyz
```
Si accedes a ella regresará un *ok*, esto significa que está funcionando 

## Endpoints de autenticación 
### Login
```bash
POST /api/v1/user/login
```
Tienes que enviar el siguiente `body`
```json
{
  "email": "user@gmail.com",
  "password": "12345"
}
```
### Crear usuario
```bash
POST /api/v1/user/create
```
`body`
```json
{
  "name": "luisedoccor",
  "password": "123456",
  "email": "luiseduardoocegueda@gmail.com"
}
```
En el caso de que fue `exitoso`, ambos enviara una respuesta igual a esta *(obviamente cambiando el token)*
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c"
}
```
De lo contario enviaría lo siguiente:
```json
{
  "msg": "Explicación del error"
}
```
#### También en caso de errores envía el código HTTP correspondiente (400, 500, 200)
A partir de ahora, en todas las peticiones que hagas deberás enviar el token en el header de la solicitud,
ya que con eso se obtendrá el ID del usuario para gestionar las tareas. Si no se envía el token,
recibirás un error de autenticación ("unauthenticated error").

## Endpoints para las tareas
### Crear tarea
```bash
POST /api/v1/task/create
```
`body`
```json
{
  "title": "Hacer Tarea",
  "content": "Actividad de mate"
}
```
`respuesta`
```json
{
  "ID": 2,
  "CreatedAt": "2024-09-26T04:32:34.214189948Z",
  "UpdatedAt": "2024-09-26T04:32:34.214189948Z",
  "DeletedAt": null,
  "title": "Hacer Tarea",
  "content": "Actividad de mate",
  "isDone": false,
  "user_id": 1
}
```
### Obtener todas las tareas
```bash
GET /api/v1/task/
```
`respuesta`
```json
[
  {
    "ID": 1,
    "CreatedAt": "2024-09-25T14:56:09.459245Z",
    "UpdatedAt": "2024-09-25T14:56:33.558287Z",
    "DeletedAt": null,
    "title": "Hacer Tarea",
    "content": "Actividad de mate",
    "isDone": false,
    "user_id": 1
  },
  {
    "ID": 2,
    "CreatedAt": "2024-09-26T04:32:34.214189Z",
    "UpdatedAt": "2024-09-26T04:32:34.214189Z",
    "DeletedAt": null,
    "title": "Hacer Tarea",
    "content": "Actividad de mate",
    "isDone": false,
    "user_id": 1
  }
]
```
### Terminar una tarea
```bash
GET /api/v1/task/finish/:id
```

### Actualizar una tarea
```bash
PUT /api/v1/task/:id
```
`body`
```json
{
  "title": "Hacer Tarea",
  "content": "Actividad de mate"
}
```

### Obtener tarea por status  (terminada o no terminada)
```bash
GET /api/v1/task/status?isdone=true
```

### Obtener tarea por ID
```bash
GET /api/v1/task/:id
```
`respuesta`
```json
{
  "ID": 2,
  "CreatedAt": "2024-09-26T04:32:34.214189948Z",
  "UpdatedAt": "2024-09-26T04:32:34.214189948Z",
  "DeletedAt": null,
  "title": "Hacer Tarea",
  "content": "Actividad de mate",
  "isDone": false,
  "user_id": 1
}
```
### Borrar tarea
```bash
DELETE /api/v1/task/:id
```
## En el caso de todas aquellas peticiones que tienen id como un parámetro, si no se encuentra algo con ese, id, la respuesta será la siguiente
```json
{
  "msg": "Invalid ID"
}
Todas las respuestas van acompañadas de su código HTTP correspondiente
```
