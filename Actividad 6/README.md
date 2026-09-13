# Tarea: Backend con Node.js, Express y MongoDB

**Fecha de entrega:** Lunes 14 de septiembre

**Temas:** Peticiones HTTP, JWT, CRUD, Middleware, Node.js, MongoDB, MongoDB Atlas y Mongoose

> Versión en Markdown del archivo `Tarea- Backend con Node.js, Express y MongoDB.docx`, para poder visualizarla directamente en GitHub.

---

## 1. ¿Qué son las peticiones HTTP y para qué sirven?

Las peticiones HTTP son mensajes que se envían entre un cliente y un servidor para solicitar o enviar información a través de Internet.

Por ejemplo, cuando una aplicación necesita consultar los datos de un usuario, el frontend realiza una petición al backend. El servidor recibe la petición, procesa la información y devuelve una respuesta.

Los principales métodos HTTP son:

| Método | Función | Ejemplo |
|--------|---------|---------|
| GET | Obtener información | Consultar una lista de usuarios |
| POST | Crear información | Registrar un nuevo usuario |
| PUT | Actualizar información | Modificar los datos de un usuario |
| PATCH | Actualizar parcialmente | Cambiar solamente el correo |
| DELETE | Eliminar información | Eliminar un usuario |

### Ejemplo en Express

```js
app.get("/usuarios", (req, res) => {
    res.json({
        mensaje: "Lista de usuarios"
    });
});
```

Cuando el cliente realiza una petición GET a `/usuarios`, el servidor responde con un mensaje.

---

## 2. ¿Qué es JWT (JSON Web Token)?

JWT significa **JSON Web Token**. Es un estándar utilizado para transmitir información de manera segura entre diferentes partes de una aplicación. Uno de sus usos más comunes es la **autenticación de usuarios**.

Por ejemplo, cuando un usuario inicia sesión:

1. El usuario envía su correo y contraseña.
2. El servidor verifica las credenciales.
3. Si son correctas, el servidor genera un JWT.
4. El usuario recibe el token.
5. En las siguientes peticiones, el usuario envía ese token.
6. El servidor verifica el token antes de permitir el acceso a determinadas rutas.

### Ejemplo de creación de un JWT

```js
const jwt = require("jsonwebtoken");

const token = jwt.sign(
    { id: usuario.id },
    "clave-secreta",
    { expiresIn: "1h" }
);

console.log(token);
```

### Verificación del token

```js
const datos = jwt.verify(token, "clave-secreta");
console.log(datos);
```

De esta manera, JWT permite identificar al usuario que está realizando una petición y proteger determinadas rutas del backend.

> **Importante:** en una aplicación real, la clave secreta no debe escribirse directamente en el código. Se recomienda utilizar variables de entorno.

---

## 3. ¿Qué es un CRUD?

CRUD es un acrónimo que representa las cuatro operaciones básicas que se pueden realizar sobre los datos de una aplicación:

- **C - Create:** Crear
- **R - Read:** Leer
- **U - Update:** Actualizar
- **D - Delete:** Eliminar

Por ejemplo, en un sistema de usuarios:

```
POST    /usuarios       → Crear un usuario
GET     /usuarios       → Obtener todos los usuarios
GET     /usuarios/:id   → Obtener un usuario
PUT     /usuarios/:id   → Actualizar un usuario
DELETE  /usuarios/:id   → Eliminar un usuario
```

### Ejemplo básico de CRUD en Express

```js
const express = require("express");
const app = express();
app.use(express.json());

let usuarios = [];

app.post("/usuarios", (req, res) => {
    const usuario = req.body;
    usuarios.push(usuario);
    res.status(201).json({
        mensaje: "Usuario creado",
        usuario
    });
});

app.get("/usuarios", (req, res) => {
    res.json(usuarios);
});

app.put("/usuarios/:id", (req, res) => {
    const id = Number(req.params.id);
    usuarios[id] = req.body;
    res.json({
        mensaje: "Usuario actualizado",
        usuario: usuarios[id]
    });
});

app.delete("/usuarios/:id", (req, res) => {
    const id = Number(req.params.id);
    usuarios.splice(id, 1);
    res.json({
        mensaje: "Usuario eliminado"
    });
});

app.listen(3000, () => {
    console.log("Servidor ejecutándose en el puerto 3000");
});
```

Este ejemplo permite realizar las cuatro operaciones principales de un CRUD.

---

## 4. ¿Qué son los Middleware?

Un **middleware** es una función que se ejecuta durante el proceso de una petición HTTP, antes de que esta llegue a la respuesta final.

Los middleware pueden utilizarse para diferentes tareas, como:

- Verificar autenticación
- Validar información
- Registrar peticiones
- Procesar datos
- Controlar permisos
- Manejar errores

El flujo puede representarse de la siguiente manera:

```
Cliente
   ↓
Petición HTTP
   ↓
Middleware
   ↓
Ruta
   ↓
Respuesta
```

### Ejemplo de Middleware

```js
const logger = (req, res, next) => {
    console.log(req.method, req.url);
    next();
};

app.use(logger);
```

En este ejemplo, el middleware muestra en la consola el método HTTP y la dirección solicitada. La función `next()` es importante porque permite que la petición continúe hacia el siguiente middleware o hacia la ruta correspondiente.

### Ejemplo de Middleware para verificar un token

```js
const verificarToken = (req, res, next) => {
    const token = req.headers.authorization;
    if (!token) {
        return res.status(401).json({
            mensaje: "No autorizado"
        });
    }
    next();
};
```

Este middleware puede utilizarse para proteger una ruta:

```js
app.get("/perfil", verificarToken, (req, res) => {
    res.json({
        mensaje: "Bienvenido a tu perfil"
    });
});
```

---

## 5. ¿Cómo se comunica Node.js con diferentes archivos?

En proyectos de Node.js es recomendable dividir el código en diferentes archivos para mantener una estructura organizada.

Un proyecto puede tener una estructura como:

```
backend/
│
├── server.js
│
├── routes/
│   └── usuarios.js
│
├── controllers/
│   └── usuariosController.js
│
├── models/
│   └── usuario.js
│
└── middleware/
    └── auth.js
```

Los archivos pueden comunicarse mediante módulos utilizando `require` y `module.exports`, o utilizando la sintaxis moderna de `import` y `export`.

### Ejemplo

Archivo `usuarios.js`:

```js
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
    res.json({
        mensaje: "Lista de usuarios"
    });
});

module.exports = router;
```

Después, desde `server.js`:

```js
const usuariosRoutes = require("./routes/usuarios");
app.use("/usuarios", usuariosRoutes);
```

De esta manera, `server.js` puede utilizar las rutas que se encuentran en otro archivo. Separar el proyecto en archivos permite que el código sea más fácil de leer, mantener y modificar.

---

## 6. ¿Qué son las bases de datos no relacionales?

Las bases de datos no relacionales, también conocidas como **NoSQL**, son sistemas de almacenamiento de información que no utilizan necesariamente tablas relacionadas como las bases de datos relacionales tradicionales.

En una base de datos relacional como MySQL, la información normalmente se organiza en:

```
Base de datos
    ↓
Tablas
    ↓
Filas y columnas
```

En una base de datos documental como MongoDB, la información se organiza principalmente mediante:

```
Base de datos
    ↓
Colecciones
    ↓
Documentos
    ↓
Campos
```

Un documento puede tener una estructura similar a JSON:

```json
{
    "nombre": "Andrea",
    "edad": 30,
    "correo": "andrea@email.com"
}
```

Una característica importante de las bases de datos NoSQL es que pueden ofrecer una estructura más flexible para determinados tipos de aplicaciones.

---

## 7. ¿Qué es MongoDB?

**MongoDB** es una base de datos NoSQL orientada a documentos. En lugar de almacenar los datos principalmente en tablas y filas, MongoDB utiliza **colecciones y documentos**.

Por ejemplo, una colección llamada `usuarios` podría contener documentos como:

```json
{
    "nombre": "Carlos",
    "correo": "carlos@email.com",
    "edad": 25
}
```

Otro documento podría ser:

```json
{
    "nombre": "Laura",
    "correo": "laura@email.com",
    "edad": 28
}
```

MongoDB almacena internamente estos documentos utilizando **BSON**, una representación binaria de documentos con una estructura similar a JSON. MongoDB es utilizado frecuentemente en aplicaciones web porque se integra fácilmente con tecnologías como Node.js y Express.

---

## 8. ¿Qué es MongoDB Atlas?

**MongoDB Atlas** es un servicio en la nube que permite utilizar MongoDB sin tener que instalar y administrar personalmente un servidor de base de datos. Para comenzar a utilizarlo se puede crear una cuenta y utilizar uno de los planes gratuitos disponibles.

Los pasos generales son:

1. Crear una cuenta en MongoDB Atlas.
2. Crear un proyecto.
3. Crear un clúster.
4. Configurar el acceso a la base de datos.
5. Crear un usuario para la base de datos.
6. Obtener la cadena de conexión.
7. Conectar el backend de Node.js con MongoDB.

La conexión normalmente se realiza mediante una cadena de conexión proporcionada por MongoDB Atlas.

---

## 9. ¿Qué es Mongoose?

**Mongoose** es una biblioteca de Node.js que facilita el trabajo con MongoDB. Permite crear **Schemas** y **Models**, además de proporcionar herramientas para validar y manipular los datos.

### Ejemplo de instalación

```bash
npm install mongoose
```

### Crear un Schema

```js
const mongoose = require("mongoose");

const usuarioSchema = new mongoose.Schema({
    nombre: String,
    correo: String,
    edad: Number
});
```

### Crear un Model

```js
const Usuario = mongoose.model("Usuario", usuarioSchema);
module.exports = Usuario;
```

El modelo `Usuario` permite realizar operaciones sobre los documentos correspondientes a los usuarios.

---

## 10. Ejemplos de Mongoose

### Crear un usuario

```js
const usuario = new Usuario({
    nombre: "Andrea",
    correo: "andrea@email.com",
    edad: 30
});
await usuario.save();
```

### Obtener todos los usuarios

```js
const usuarios = await Usuario.find();
```

### Buscar un usuario por ID

```js
const usuario = await Usuario.findById(id);
```

### Actualizar un usuario

```js
await Usuario.findByIdAndUpdate(id, { edad: 31 });
```

### Eliminar un usuario

```js
await Usuario.findByIdAndDelete(id);
```

Estas operaciones corresponden directamente a las operaciones de un CRUD.

---

## 11. Relación entre Node.js, Express, Mongoose y MongoDB

Todas estas tecnologías pueden trabajar juntas dentro de un backend.

```
             CLIENTE
                │
                │ Petición HTTP
                ↓
             EXPRESS
                │
                ↓
           MIDDLEWARE
                │
                ↓
              RUTA
                │
                ↓
           CONTROLADOR
                │
                ↓
            MONGOOSE
                │
                ↓
             MONGODB
                │
                ↓
          MONGODB ATLAS
```

Por ejemplo, un usuario puede enviar `POST /usuarios` con información como:

```json
{
    "nombre": "Andrea",
    "correo": "andrea@email.com",
    "edad": 30
}
```

Express recibe la petición, el controlador procesa los datos y Mongoose los guarda en MongoDB.

---

## Conclusión

Las peticiones HTTP permiten la comunicación entre el cliente y el servidor. Express facilita la creación de servidores y rutas en Node.js, mientras que los middleware permiten procesar y controlar las peticiones antes de entregar una respuesta.

El CRUD representa las operaciones básicas para trabajar con información: crear, consultar, actualizar y eliminar. JWT permite implementar mecanismos de autenticación y proteger rutas del backend.

Por otro lado, MongoDB es una base de datos NoSQL orientada a documentos. MongoDB Atlas permite utilizar MongoDB en la nube y Mongoose facilita la conexión entre Node.js y MongoDB mediante Schemas y Models.

El uso conjunto de **Node.js, Express, JWT, Mongoose y MongoDB** permite desarrollar backends modernos capaces de recibir peticiones, autenticar usuarios, procesar información y almacenarla de manera organizada.

---

**Autor:** Andrea Rodríguez
