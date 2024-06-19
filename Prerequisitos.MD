# Pasos 


# Requisitos previos
1. **Acceso a la Cuenta del Cliente**: Es indispensable contar con acceso a la cuenta del cliente, ya sea a través de SSO con claves de acceso temporales o mediante un usuario IAM con claves de acceso generadas. Este acceso debe estar garantizado con suficiente antelación al proceso de despliegue. Se sugiere faguero@morrisopazo, pfalcon@morrisopazo.com como posibles candidatos, consultar con antelacion al team tecnico a quien se le otorgan las credenciales


2. **Dominio Disponible**: El cliente debe haber adquirido el dominio donde se alojará la aplicación o contar con un subdominio adecuado, por ejemplo, "chatbot.minegocio.com". En caso de no disponer de uno, se deberá realizar la compra a través del servicio AWS Route 53, lo cual puede hacerse de forma independiente o con nuestra asistencia. Si brindamos asistencia, será necesario disponer con antelación de los datos del comprador, como nombre, apellido, dirección, entre otros, para agilizar el trámite. Además, la cuenta de correo electrónico proporcionada debe pertenecer a alguien que esté participando en este proceso, ya que será necesario responder a un correo electrónico haciendo clic en un enlace.


3. **Actividad en Cuentas de AWS Nuevas**: Para cuentas de AWS nuevas, es un requisito previo generar alguna actividad que demuestre que la cuenta está activa. La opción recomendada es crear una máquina virtual en el servicio AWS EC2 durante un tiempo mínimo que genere un gasto ínfimo en la cuenta destino de Chatbot Go. Sin esta actividad, no es posible comprar dominios ni generar certificados, entre otras cosas. En este sentido tambien podemos proporcionar ayuda si llegara a ser necesario











## 1er Paso en la infra del cliente

## Escenario 1 :
   

2) Firma de modelos AWS Bedrock que usa la aplicacion ChatbotGO

   a. Diríjase al servicio de Bedrock dentro de la cuenta del cliente.
   b. En el menú izquierdo busque la opción Model access
   c. Deberá solicitar acceso a los siguientes modelos:
       * Amazon -> Titan Embeddings G1 - Text
       * Anthropic -> Claude
       * Anthropic -> Claude Instant
   
 
      Para el caso específico de los modelos Anthropic es necesario realizar una solicitud mediante un formulario, aquí se pedirán los siguientes datos:

       Nombre de la empresa (cliente)
       Rubro
       URL de su sitio web
       Motivo de la solicitud: “We want to deploy a chatbot”

   En el caso aparezca un error que no deje firmar los modelos seleccionados es muy posible que sea porque la cuenta es nueva y no registra gastos. Para esto levante una instancia EC2 t2.small durante 15 minutos y vuelva a intentar firmar los modelos.


3) Adquisición y Configuración de Dominio
   Por motivos de agilización en la integración de la solución con un dominio, es estrictamente necesario que este se gestione desde la consola AWS. Existirán dos escenarios: uno donde el cliente ya contará con un dominio comprado y otro donde se requiera realizar la compra de un nuevo dominio.
   Deberemos dirigirnos al servicio Route 53, en el menú de la izquierda seleccionaremos Registered Domains.
   Aquí será preciso verificar si el cliente cuenta o no con dominios adquiridos, y si desea usar alguno de estos para desplegar la solución como subdominio. O por lo contrario, se requiere adquirir un nuevo dominio.




8) Chequear si en la cuenta del cliente tiene los recursos diesponibles para la instalacion
   * Loguearse con las credenciales via __aws cli__
   * Ejecutar
 

  
             ./cust_infra_check.sh
2) Verificar la existencia del subdominio donde se va a referenciar la aplicacion

        ./cust_subdoman_check.sh subdomain.domain.com

   