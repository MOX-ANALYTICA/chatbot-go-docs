# 20-02-01 Gestión de Usuarios y Grupos
## 1. Usuarios
### 1.1. Tipos de Usuario
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

### 1.2. Creación de un nuevo usuario
1. Diríjase al menú de administración presionando la burbuja con la inicial de su nombre de usuario en la parte superior.
2. Seleccione la opción **Usuarios**.
3. Encontrará dos pestañas: **Administrar Usuarios** y **Crear Usuarios**, seleccione esta última.
4. Ingrese los datos de nombre de usuario y contraseña temporal.
5. Finalmente presione el botón crear.

> **Nota**  
> - La primera vez que el nuevo usuario inicie sesión con las credenciales asignadas, se le solicitará cambiar su contraseña antes de poder hacer uso de la aplicación.

### 1.3. Eliminación de usuarios
1. Nuevamente diríjase al menú de administración presionando la burbuja con la inicial de su nombre de usuario en la parte superior.
2. Seleccione la opción **Usuarios**.
3. Encontrará dos pestañas: **Administrar Usuarios** y **Crear Usuarios**, quédese en la primera opción.
4. La vista consiste en una barra de búsqueda y la lista completa de usuarios, puede intentar buscar el usuario que se desea eliminar.
5. Presione el ícono de papelera y confirme la acción.

> **Nota**  
> - Esta acción eliminará el usuario, quien ya no tendrá acceso a la aplicación, pero conservará su historial de conversaciones actual.

## 2. Grupos
Para lograr una gestión efectiva del nivel de acceso de usuarios a la aplicación, estos se organizan en dos grupos principales:
- **admin:** usuarios con privilegios de administrador, tienen acceso a gestionar usuarios, documentos, perfiles y asociaciones.
- **user:** usuarios con credenciales, unicamente tienen acceso a sus conversaciones con el bot.

### 2.1. Gestión de Grupos
1. Diríjase al menú de administración presionando la burbuja con la inicial de su nombre de usuario en la parte superior.
2. Seleccione la opción **Grupos**
3. Encontrará los dos grupos principales mencionados anteriormente junto a un ícono para edición de estos.
4. Seleccione el grupo **user** y presione el botón de edición.
5. Encontrará "marcados" los usuarios que pertenecen a este grupo actualmente, e inmediatamente debajo de estos la lista completa de usuarios de la aplicación, también puede utilizar la barra de búsqueda.
6. Seleccione o deseleccione los usuarios que desea incluir o eliminar del grupo, también existe un ícono de papelera para eliminar los usuarios.
7. Además de esto, también puede actualizar la descripción del grupo.
8. Si desea guardar los cambios hechos, diríjase a la parte inferior de este modal y presione **Guardar cambios**, para descartar los cambios presione **Cancelar**.
