> **Importante**  
> - La siguiente documentación de la integración con Meta está estrictamente enfocada en cuentas de Facebook activas y con negocios **verificados**.
> - Si no cuenta con un perfil verificado y una app creada, siga los pasos de la guía de esta misma documentación [WhatsApp - 1 Verificación de Portfolio Comercial](https://github.com/morrisopazo/chatbot-go-docs/wiki/WhatsApp-%E2%80%90-1-Verificaci%C3%B3n-Portfolio-Meta)

# 7.2.1 Configuración Aplicación Developers Meta
1. Vuelve a la consola de administración de Go en [meta.developers/apps](https://developers.facebook.com/apps/)
2. Ahora ingresa en la configuración de WhatsApp, selecciona el portfolio comercial que creamos en la sección anterior.
3. Ahora seleccione la siguiente opción para abrir la ventana de gestión de API de WhatsApp.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f1308c96-cfb7-4ca9-a3ba-e3c5dc5f1f06" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/0825e7ca-ffc2-4e4f-9100-49ff3d3c9d01" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/10e64c6d-03cb-4f3e-aa5b-811918e6225b" />
</p>

# 2 Habilitar Número de WhatsApp

> **Nota**  
> - Las siguientes instrucciones se enfocan en preparar un número de prueba. Esta no es la configuración definitiva para la puesta en productivo.

1. Dirigirse, en el mismo menú de **WhatsApp/Configuración**, agregar la suscripción a **messages** como se muestra a continuación.
2. Finalmente, debe agregar un número en la sección **Para**, con el fin de probar el servicio de mensajería de **WhatsApp** con este usuario.

<p align="center">
  <img src="https://github.com/user-attachments/assets/817ee89f-c252-4963-b729-e7cbd6c1aeaf" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/004b2302-d400-46b8-a918-d704e8839f5e" />
</p>

# 7.2.3 Datos para SecretsManager
1. Para completar la integración de Whatsapp con Meta necesitará configurar los siguientes datos:
    a. **APP_ID**: identificador de la aplicación
    b. **APP_SECRET**: clave secreta de la aplicación
    c. **META_TOKEN**: token de acceso de meta (permanente o temporal)
    d. **VERIFY_TOKEN**: token de verificación al inscribir un usuario
    e. **VERSION**: un flag para activar el bot en la cuenta, deberá introducir un número distinto.

2. Para obtener los datos **APP_ID** y **APP_SECRET**, diríjase a la siguiente pantalla, deberá ingresar su contraseña de Facebook para mostrar la clave secreta.

<p align="center">
  <img src="https://github.com/user-attachments/assets/41a4af52-c510-4159-a535-a17abe32f61e" />
</p>

3. Ahora diríjase a la pantalla de configuración de API, aquí presione el botón **Generar un Token** y siga los pasos indicados para hacerlo. Este valor nos servirá para el campo **META_TOKEN**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e62af66f-0f90-4407-ae05-32b6a1430e4b" />
</p>

4. Diríjase al servicio de **AWS/Secretsmanager** y actualice los valores almacenados en los secretos de **chat/integration-meta** como se muestra a continuación.
Observe que necesita modificar el parámetro **VERSION** para que la app detecte el cambio. También, el parámetro **VERIFY_TOKEN** debe ser generado por el usuario, un valor aleatorio basta, por ejemplo: *META_1234ASDFG*.

<p align="center">
  <img src="https://github.com/user-attachments/assets/4f3db013-53bb-4b51-89e1-d3778a93749c" />
</p>

5. De ser necesario, haga un “Force Deployment” al servicio the integration-meta en ECS. Y espere hasta que el servicio esté operativo.
6. Finalmente diríjase a la pantalla Configuración de Webhook, introduzca aquí el VERIFY_TOKEN que creó y la url de meta de la siguiente forma: https://api.example-domain.com/meta/webhook.
7. Si por alguna razón esta verificación falla, revise que el servicio de Meta está activo en ECS y Healthy, de ser ese el caso, espere un momento y vuelva a intentarlo.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f90281ec-2548-4965-be0a-1217fba6700a" />
</p>

# 7.2.4 Puesta en Productivo
## 7.2.4.1 Registro de Números
Debe contar con un número de tu propiedad, con código de país /área y con acceso a llamadas y SMS.

> **Importante**  
> El número que elegirá para usar no debe contar con una cuenta vinculada de WhatsApp o WhatsApp Business, deberá eliminar estas cuentas si desea configurar este número con los pasos siguientes.

1. Dirigirse a [meta.developers/apps](https://developers.facebook.com/apps/), seleccione la app que configuró.
2. En el menú de la izquierda seleccione **WhatsApp > Configuración de API**
3. Baje hasta el final de la página, en el Paso 5 haga clic en el botón **Agregar número de teléfono.**

<p align="center">
  <img src="https://github.com/user-attachments/assets/195fea51-d0ee-483b-9ab2-8056d21c8f36" />
</p>

4. Siga las instrucciones de la ventana para configurar el número de teléfono con los datos de su empresa.
5. Se solicitará la verificación del número, puede recibir el código generado mediante mensaje de texto o llamada.
6. Ingrese el código obtenido y complete el registro de su número

<p align="center">
  <img src="https://github.com/user-attachments/assets/c4fc443b-9072-4071-8351-ddb85b205179" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3c920840-c6d4-47d8-aca7-80cc0a261440" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/323a01de-b4f7-4759-a75a-3b316067ae7c" />
</p>

7. Observará que el número que acaba de incluir muestra el estado de “Pendiente”, será necesario **verificar** el número agregado.
8. Haga clic sobre el número registrado y diríjase a la pestaña **Perfil**. Aquí podrá modificar el nombre que aparecerá como contacto, pronto le llegará un correo indicando que el nombre fue aprobado.

<p align="center">
  <img src="https://github.com/user-attachments/assets/23c3d49f-18b3-4394-ae97-85b8157b372c" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/9113068e-a970-483b-89eb-521ea51a5bdc" />
</p>

## 7.2.4.2 Activar Nuevo Número
El proceso de activación, o registro, de un número fue realizado siguiendo las siguientes instrucciones oficiales [meta.docs/cloud-api/whatsapp-activation](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/registration).

1. Para activar el número debemos dirigirnos a la consola de desarrollador desde [meta.developers/apps](https://developers.facebook.com/apps/). 
2. Diríjase a **Configuración de la app > Básica**,  encontrará los detalles de la aplicación. Aquí, incluya el link directo a los términos y condiciones de su empresa, finalmente presione el botón de **Guardar Cambios**.
3. Ahora haga clic en el botón superior para activar el modo en productivo de la app.
4. Ahora deberá realizar una solicitud POST, incluyendo el token temporal generado en la consola [meta.developers/apps](https://developers.facebook.com/apps/) y el número de teléfono de prueba. Puede obtener la UR y el token de acceso desde la consola de Meta.

<p align="center">
  <img src="https://github.com/user-attachments/assets/be5b6b4b-ca3d-4eb7-814e-b1db1ac8d6dc" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/462fa06f-0727-4de3-b894-485db6a17259" />
</p>

5. Estructure su solicitud POST de la siguiente forma:
```
curl -i -X POST https://graph.facebook.com/v21.0/<generated-id>/messages \
-H 'Authorization: Bearer <access-token>' \
-H 'Content-Type: application/json' \
-d '{ 
   "messaging_product": "whatsapp", 
   "to": "<your-phone-number>",
   "type": "text", 
   "text": {
         "body": "Hello world"
    } 
}'
```
6. Finalmente, observará en la consola [meta.business/whatsapp-manager/phone-numbers](https://business.facebook.com/latest/whatsapp_manager/phone_numbers) que el número fue aprobado, además, su cuenta de whatsapp habrá sido activada.

<p align="center">
  <img src="https://github.com/user-attachments/assets/e62c6fea-b2f6-4cc0-8032-063ccab17d2e" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/b578cb19-7d78-448c-bff1-e71b07b03008" />
</p>

# 7.2.5 Token Permanente
1. Dirigirse a la consola de [meta.business/whatsapp-manager](https://business.facebook.com/latest/whatsapp_manager/), en el menú de la izquierda inferior presionar la opción de **Configuración/Personas**.
2. Aquí podrá invitar a los desarrolladores para que ejecuten la integración con Facebook Meta.

<p align="center">
  <img src="https://github.com/user-attachments/assets/ff9dc6ce-c937-4a0c-90c8-2cf84f93f95c" />
</p>

3. A continuación diríjase a **usuarios del sistema**. Aquí cree un usuario del sistema, asigne un rol de **Admin** al usuario.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0719de98-f8a3-401a-bdc5-c4b641c96796" />
</p>

4. Haga clic en los tres puntos del usuario de sistema, y seleccione **Asignar Activos**.

<p align="center">
  <img src="https://github.com/user-attachments/assets/bba9507d-d5f0-42f8-a9d6-dc98acef76a0" />
</p>

5. Dentro del menú de **Asignar Activos**, elija la aplicación creada para la integración de WhatsApp y presione el botón de confirmación.

<p align="center">
  <img src="https://github.com/user-attachments/assets/527be222-5d5c-42e6-8c25-06cb193f6316" />
</p>

6. Selecciona el usuario del sistema en el botón **Detalles**, aquí presiona el botón **Generar Token** y sigue los pasos.

<p align="center">
  <img src="https://github.com/user-attachments/assets/1d3860eb-e0e4-4735-98f7-4a53ef437c35" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/eb2ef6e5-2e22-4e89-86d8-c51faadedf03" />
</p>

7. Asigna el permiso **whatsapp_business_messaging** al token que se generará.

<p align="center">
  <img src="https://github.com/user-attachments/assets/8cd39840-0703-414b-bc01-8c95887eebdd" />
</p>

8. Finalmente, copie el token e insértelo en el campo **META_TOKEN** en el servicio de SecretsManger.

<p align="center">
  <img src="https://github.com/user-attachments/assets/74f6e3fa-c503-46b7-958d-e22483cfc128" />
</p>