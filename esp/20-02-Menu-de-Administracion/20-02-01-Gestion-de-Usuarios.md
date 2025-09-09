# 20-02-01 Gestión de Usuarios y Grupos
# 1. Usuarios
# 1.1. Tipos de Usuario
**Guest (Invitado)**
- No requiere credenciales para interactuar.
- Almacena pero no accede a su historial de conversaciones.
- Puede interactuar con el bot de la misma forma que un usuario convencional, se consultarán los documentos cargados.

**Usuario**
- Acceso mediante credenciales.
- Almacena y puede acceder al historial de sus conversaciones.

**Admin (Administrador)**
- Todas las capacidades del usuario común.
- Capacidad de cargar y borrar archivos que alimentan el modelo de la aplicación.
- Administración de credenciales de otros usuarios.
- Capacidad de configuración de la integración con WhatsApp.
- Capacidad para ver el estado de la aplicación y reiniciar los servicios en caso de fallo.

# 1.2. Creación de un nuevo usuario
1. Diríjase al menú presionando el botón **"..."** en la parte inferior.
2. Seleccione la opción **"Administración de Usuarios"**.
3. Se encontrará en la pestaña **"Crear Usuarios"**, ingrese los datos requeridos.

> **Nota**  
> - La primera vez que el nuevo usuario inicie sesión con las credenciales asignadas, se le solicitará cambiar esta contraseña antes de poder hacer uso de la aplicación

<p align="center">
  <img src="https://github.com/MOX-ANALYTICA/chatbot-go-docs/blob/main/assets/go_usermenu_ESP.png" />
</p>

Si el usuario ya existe, puede realizar algunos cambios sobre él como administrador. Para esto diríjase a la pestaña **"Administrar Usuarios"** e introduzca el nombre de usuario correspondiente.

<p align="center">
  <img src="https://github.com/MOX-ANALYTICA/chatbot-go-docs/blob/main/assets/go_usermenu_admin_ESP.png" />
</p>

# 2. Grupos
# 2.1. Gestión de Usuarios