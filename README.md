# lab-user-signup

Crear la experiencia descrita en el diagrama.

Una página inicial en `/` con un enlace a `/signup` para registrarse.

Una página de registro en `/signup` con un formulario para completar email y password.

Al enviar el formulario, se registrará un nuevo usuario en la base de datos. No olvides cifrar la contraseña antes de guardar el usuario!!!. Si durante la creación ocurre algún error en la validación de errores, debe mostrarse el mismo formulario mostrando los datos utilizados y mensajes de error.

Si el usuario se crea con éxito, se navega a la página de perfil o detalle del usuario `/users/ID` donde se mostraran los datos del usuario con id = ID así como un enlace para editar (`/users/ID/edit`) y un botón para eliminar el usuario (`/users/ID/delete`).

![Guide](./guide.png?raw=true "Guía")

## Iteración 2 - Mongoose middlewares

Mantener el mismo funcionamiento de la aplicación pero llevando la lógica de cifrado de contraseña al modelo de usuario, haciendo uso del middlware [pre save](https://mongoosejs.com/docs/middleware.html#pre)

Añadir un [método al modelo de usuario](https://mongoosejs.com/docs/guide.html#methods) que reciba una contraseña en claro y devuelva una promesa que resuelva con un valor booleano: `true` si la contraseña es _equivalente_ a la contraseña cifrada, `false` en caso contario.

## Iteración 3 - Login

Añadir ruta `GET /login` que devuelva un formulario con el que iniciar sesión en el sistema enviando email y contraseña mediante `POST /login`.

Añadir ruta `POST /login` que reciba email y contraseña en el _body_ de la petición, busque el usuario con el email indicado en la base de datos y compruebe que la contraseña recibida corresponde con ese usuario, utilizando el método implementado en la Iteración 2. Si no se reciben ambos email y contraseña, no se encuentra un usuario con el email indicado o la contraseña no es válida, se deberá devolver el mismo formulario de _login_ pero mostrando mensajes de error.

Si las credenciales recibidas son correctas se deberá almacenar una nueva sesión en el sistema, generando un ID de sesión aleatorio y asociandolo al ID del usuario identificado. El ID de sesión generado y almacenado deberá devolverse al cliente en la cabecera `Set-Cookie` junto con una redirección a la página principal `/`.

## Iteración 4 - Identificar usuario autenticado

Para cada petición recibida en el sistema, mostrar un log indicando el email del usuario que realiza la petición. Identificaremos al usuario al recibir una cabecera `Cookie` en la petición con el valor `sessionId=xxx`, habiendo registrado previamente el ID de sesión `xxx` en el sistema, asociado al ID del usuario en cuestión.

Si la petición no contiene la `Cookie`, o no se encuentra una sesión registrada, se mostrará el log `usuario anónimo`.

Para que esta lógica esté presente en todas las peticiones, será interesante programar un [middleware en express](https://expressjs.com/en/guide/using-middleware.html#middleware.application). El middleware implementado deberá almacenar dentro de los objectos `request` y `response` una referencia al usuario identificado para poder acceder desde un middleware posterior o desde una vista hbs.

Por último, mostrar en todas las vistas de la aplicación, el mensaje `Welcome, <email>` con el email del usuario que realiza la petición.

## Iteración 5 - Rutas privadas

Restringir el acceso a todas las rutas salvo las de `/login` y `/signup` para que únicamente usuarios autenticados puedan acceder. Si la petición a una ruta privada no está autenticada, dirigir al usuario a la ruta `/login` con un código HTTP 401. Para esta última iteración, implementar un middleware a nivel de ruta que haga uso del usuario almacenado en el objeto `request` por el middleware implementado en la Iteración 4.

-

A por ello!!
