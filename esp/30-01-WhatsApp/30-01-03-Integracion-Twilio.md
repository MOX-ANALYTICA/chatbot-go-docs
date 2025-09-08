# 7.3.1 Características Generales
- Rapidez en configuración
- Documentación clara y completa
- Soporte a cliente
- Capacidades variadas de interacción por medio de whatsapp
Uso de la API oficial de Meta WhatsApp
## 7.3.1.1 Seguridad
Twilio soporta comunicaciones seguras y encriptadas a través del protocolo HTTPS. Twilio no emitirá un certificado TLS/SSL, por lo que esto debe hacerse desde el proveedor de dominio adquirido.

Twilio también hace uso de tokens de acceso para las interacciones con las herramientas de SDKs, voz, conversaciones, y video. Estos son tokens de corta duración que autentican las solicitudes de parte del cliente.

**Fuentes:**
- https://security.twilio.com/
- https://www.twilio.com/en-us/security
- https://www.twilio.com/docs/usage/security

## 7.3.1.2 Precio
Al crear una cuenta nueva, se necesitará hacer un upgrade a esta para obtener las capacidades completas de Twilio WhatsApp. Aquí se solicitará abonar un monto mínimo de $20 además de una verificación de identidad.

Para el caso de un bot conversacional a través de Twilio, el precio aplicado será en la modalidad de **Service conversation**, así que elegiremos esta opción en la calculadora. Con una estimación de 1,000 conversaciones y 10 mensajes en cada una de estas (10,000 mensajes en total), el cobró estimado será de $50 para la región de Chile.

<p align="center">
  <img src="https://github.com/user-attachments/assets/319ef630-6491-4bc2-9c2b-beff15aafb26" />
</p>

También es recomendado activar una característica de **auto-recharge** para que la plataforma cargue un monto determinado cada vez que se alcance un monto mínimo. Podremos personalizar nuestras notificaciones al consumir estos créditos cargados.

**Fuentes:**
- https://www.twilio.com/en-us/whatsapp/pricing
- https://help.twilio.com/articles/223135607-How-do-I-set-an-automatic-payment-recharge-trigger-

# 7.3.2 Creación de cuenta y configuración
## 7.3.2.1 Requerimientos para Registro en Twilio
1. Acceso a correo para creación de la cuenta.
2. Acceso a un número de teléfono (bandeja de entrada y llamadas telefónicas).
3. Portfolio comercial verificado en plataforma Business Meta.

> **Nota**  
> Recuerde que el número de teléfono no debe estar asociado a una cuenta ya existente de Whatsapp Messaging o Whatsapp Business.

## 7.3.2.2 Upgrade de cuenta
Para ser capaces de acceder a las funcionalidades completas de Twilio, será necesario actualizar nuestra cuenta. Siga estos pasos:
1. Ingrese a su cuenta de Twilio
2. En la parte superior izquierda verá los créditos que tiene disponibles, y asu lado, el botón “Upgrade”
3. Este proceso solicitará la siguiente información:
    1. ID de persona (licencia de manejo, pasaporte, visa o identificación nacional).
    2. Información acerca de la empresa / persona individual: país, ciudad, dirección, código postal, nombre, número identificador de la empresa, página web, rubro.
    3. Información de taxes si aplica.
    4. Medio de pago para abonar a la cuenta.
4. Complete los pasos requeridos, recuerde que necesita una webcam para tomar foto de su ID.
5. Complete la información del negocio
6. Elija el monto a abonar en la cuenta, el mínimo es $20 y un máximo de $2,000
7. Le pedirá agregar un método de pago habilitado para tarjetas Visa o MasterCard.
8. Luego de realizar el pago, su cuenta contará con todas las herramientas necesarias para trabajar con Twilio.

**Fuentes:**
- https://wiki.splynx.com/addons_modules/whatsapp/upgrade-twilio

# 7.3.3 Configuración Twilio + Whatsapp
## 7.3.3.1 Creación de WhatsApp Sender
Para que seamos capaces de configurar una cuenta de whatsapp asociada a un número de teléfono propio desde Twilio es necesario crear un Whatsapp Sender. Siga estos pasos:
1. En la plataforma de Twilio, en el menú lateral izquierdo, diríjase a la opción **Messaging > Senders > WhatsApp senders**.
2. Elija la opción para registrar un número propio, también puede registrar un número de teléfono adquirido en la plataforma de Twilio.
3. A partir de este punto se le solicitará vincular su cuenta de meta, deberá seleccionar el portfolio comercial configurado en la plataforma de Meta.
4. Agregue el número de whatsapp que se utilizará con la cuenta de Whatsapp Business, se pedirá verificar este mediante una llamada telefónica o mensaje de texto.
<p align="center">
  <img src="https://github.com/user-attachments/assets/4aace6ce-f6df-45ef-b92b-68c64a4a1692" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/b0066848-af4d-4fdf-86b0-ba59c27d1eca" />
</p>
5. Finalmente, se podrán configurar webhooks, información de la cuenta de whatsapp y foto de perfil de la cuenta desde esta plataforma.
6. El estado del **Whatsapp Sender** configurado se mostrará como pendiente hasta que la plataforma de Meta pueda verificar del todo este número.
<p align="center">
  <img src="https://github.com/user-attachments/assets/ce49c3d7-b951-4387-995f-8672e95a4bdb" />
</p>
<p align="center">
  <img src="https://github.com/user-attachments/assets/91d6aebd-8786-4c32-927e-835794ae123a" />
</p>

El producto de esta configuración será un número de teléfono asociado a una nueva cuenta de Whatsapp Business, que podrá personalizar y servirá como canal de comunicación para sus clientes.

Recuerde que Twilio hace uso de la API de **Whatsapp Meta**, por lo que también será posible visualizar el número configurado desde la plataforma de **Business Meta**, el cual será gestionado a través de Twilio.
<p align="center">
  <img src="https://github.com/user-attachments/assets/3c1b2955-e265-46b3-a1a2-4571d009af7c" />
</p>

**Fuentes:**
- https://www.twilio.com/docs/whatsapp/self-sign-up

## 7.3.3.2 Creación de WhatsApp Messaging Service
Antes de poder utilizar el **WhatsApp Sender** a nivel productivo, será necesario crear un **Messaging Service**.

Puedes considerar un **Messaging Service** como una agrupación de nivel superior de funcionalidades de mensajería en torno a un conjunto común de **senders**, características y configuración. Los mismos ajustes y configuración de características se aplican a todos los **senders** (números de código largo, códigos cortos, números sin cargo, etc.) en el grupo de Messaging Services.
1. Diríjase a **Messaging > Senders > WhatsApp senders**.
2. Seleccione el WhatsApp sender creado e ingrese en su pantalla de configuración.
3. Verá en la parte superior de la pantalla de configuración un selector con el título **Messaging Service**, y a su lado un link azul con la opción para crear un **Messaging Service**.
<p align="center">
  <img src="https://github.com/user-attachments/assets/f83dcdc6-db97-4e4d-966b-930a7c7842a0" />
</p>

4. Presione en el link azul y siga los pasos para crear este tipo de servicio.
5. Se solicitará asignar un nombre a este servicio de mensajería.
6. También tendrá que asignar el **WhatsApp Sender** configurado a la **Sender Pool** de este servicio.
7. Existen configuraciones adicionales que puede omitir por el momento.
8. El servicio habrá sido creado.
9. Ahora nuevamente diríjase al campo mostrado en el paso 3, seleccione el Messaging service que acaba de crear.
<p align="center">
  <img src="https://github.com/user-attachments/assets/a2859999-a7ca-414c-b8c7-2dff91c5be77" />
</p>

## 7.3.3.3 Integración de Webhook
Para capturar los eventos de entrada de mensajes de usuarios y responder mediante una lógica personalizada, es necesario habilitar webhooks de respuesta y de verificación de estado del servicio.

Los eventos que podemos capturar al recibir o enviar distintos tipos de mensaje a través de Whatsapp son los siguientes:
- Mensajes de texto
- Imágenes
- Audio
- Documentos

Cada uno de estos con atributos detallados de lo solicitado, además de acceso a la información cuando el mensaje fue enviado, recibido o leído por el usuario.
1. Diríjase a **Messaging > Senders > WhatsApp senders**.
2. Seleccione el Whatsapp sender creado e ingrese en su pantalla de configuración.
3. Encontrará los campos **Webhook URL for incoming messages** y **Fallback URL for incoming messages**, además de un **Status callback URL**.
4. Configure estos campos con la URL que habilitó para que el servicio de conversaciones fuera gestionado (asegúrese de que la comunicación sea encriptada mediante HTTPS).
5. Finalmente guarde estos cambios.
<p align="center">
  <img src="https://github.com/user-attachments/assets/6cd9b7aa-8af5-4412-9f3a-1070eb29291a" />
</p>

## 7.3.3.4 Personalización de foto de perfil e información de WhatsApp
1. Nuevamente diríjase a Messaging > Senders > WhatsApp senders.
2. Seleccione el Whatsapp sender configurado en pasos anteriores, se mostrará una ventana de configuración.
3. Baje hasta el final de esta pantalla, aquí podrá, de forma sencilla, modificar los datos de la cuenta de Whatsapp configurada.
4. La información que puede actualizar es la siguiente:
    1. Foto de perfil - formatos JPG o PNG y mayor a 640x640 pixeles.
    2. Dirección de la empresa
    3. URL de sitio web de la empresa
    4. Descripción de la empresa
    5. Rubro / Vertical
    6. Mensaje / estado de la cuenta de WhatsApp
5. Recuerde que el nombre de la empresa / nombre de la cuenta no podrá ser modificado debido a que este debe ser exactamente igual al nombre real de la empresa.

<p align="center">
  <img src="https://github.com/user-attachments/assets/8bf0ef3c-37ae-4db3-ba71-d39a896a5a65" />
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/f5748264-fe74-45af-9103-a6cfe57e411c" />
</p>