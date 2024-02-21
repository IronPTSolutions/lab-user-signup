# lab-user-signup

Crear la experiencia descrita en el diagrama.

Una página inicial en `/` con un enlace a `/signup` para registrarse.

Una página de registro en `/signup` con un formulario para completar email y password.

Al enviar el formulario, se registrará un nuevo usuario en la base de datos. No olvides cifrar la contraseña antes de guardar el usuario!!!. Si durante la creación ocurre algún error en la validación de errores, debe mostrarse el mismo formulario mostrando los datos utilizados y mensajes de error.

Si el usuario se crea con éxito, se navega a la página de perfil o detalle del usuario `/users/ID` donde se mostraran los datos del usuario con id = ID así como un enlace para editar (`/users/ID/edit`) y un botón para eliminar el usuario (`/users/ID/delete`).

![Guide](./guide.png?raw=true "Guía")
