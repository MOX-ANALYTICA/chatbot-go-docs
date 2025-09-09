# 2.1 Otorgar Acceso a Usuarios Técnicos
Para llevar a cabo el proceso de despliegue de Mox AI Chat, es indispensable contar con acceso a la cuenta del cliente. Este acceso puede gestionarse de las siguientes maneras:

1. **Cuenta SSO (recomendado)**: Utilizando un sistema de Single Sign-On, es la forma de acceso más segura ya que hace uso de credenciales a corto plazo.
2. **Usuario IAM con Acceso a Consola**: Creando un usuario IAM con acceso a la consola, estas credenciales son de largo plazo y no proponen una medida de seguridad robusta.

> **Nota**  
> - Es esencial que este acceso esté garantizado con suficiente antelación al proceso de despliegue, es importante coordinar con el equipo técnico previamente para determinar quién contará con el acceso a la cuenta.

## 2.1.1 Creación de Políticas de Acceso Personalizadas
Antes de crear el acceso para los técnicos, se solicitará que cargue políticas personalizadas siguiendo el principio de mínimos privilegios.
1. El equipo técnico se pondrá en contacto con usted, cargue las políticas compartidas en [IAM > Policies](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/policies)
2. Recuerde hacerlo en dos políticas independientes, de la misma forma que se compartieron los archivos.
3. Compruebe que fueron creadas correctamente.
![image](https://github.com/user-attachments/assets/19f0ad7c-02c7-4aee-951c-c451021fe4f5)

## 2.1.2 Creación de Usuario IAM
1. Ingrese a su cuenta AWS y diríjase al servicio de [IAM > Users](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/users).
2. Cree un usuario IAM, puede ser un nombre de su preferencia *(e.g. **dev-morris**)*, asegúrese que este tendrá acceso a la consola.
![image](https://github.com/user-attachments/assets/1e607611-752d-450b-a6c6-80c81f3a007e)

3. Asigne las políticas anteriormente creadas a este usuario.
![image](https://github.com/user-attachments/assets/5469081a-f235-451b-94e0-2c63cb2d77b6)
4. Compruebe que el usuario fue correctamente creado.
5. Envíe estas credenciales al equipo técnico como un **archivo .csv**, ellos se encargarán de configurar y verificar el acceso.
![image](https://github.com/user-attachments/assets/31e803f4-81e9-40c9-b439-5aa5741409b2)

## 2.1.3 Creación de Rol de Despliegue
Los técnicos se encargarán de realizar este proceso, esta guía es informativa.
1. Diríjase al servicio [IAM > Roles](https://us-east-1.console.aws.amazon.com/iam/home?region=us-east-1#/roles) y cree un nuevo rol.
2. Seleccione en tipo de identidad **"AWS Account"**, seleccione otra cuenta e introduzca el ID de la cuenta indicada.
![image](https://github.com/user-attachments/assets/936c1d46-fce8-4c39-ac73-985afd9b87b3)

3. Nuevamente, seleccione las políticas personalizadas anteriormente generadas.
![image](https://github.com/user-attachments/assets/65f01b91-5a05-4a15-b8de-f51a4b6124fb)

4. Asigne el nombre **gh-actions-chatbot-go-role** al rol y presione el botón **Create Role**.
5. Ingrese nuevamente al rol, seleccione la pestaña **Trust Policy** y edite en formato JSON con los siguientes permisos.
```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Principal": {
				"AWS": "arn:aws:iam::ID_EXTERNAL_ACCOUNT:root"
			},
			"Action": [
				"sts:AssumeRole",
				"sts:TagSession"
			]
		}
	]
}
```
6. Finalmente compruebe que el rol fue creado correctamente.

# 2.2 Verificación de Disponibilidad de Recursos
Asegúrese de que hay disponibilidad suficiente para los recursos necesarios en la región donde se va a desplegar Mox AI Chat Esto incluye las siguientes cuotas de servicios:

|          Recurso          | Cuota por Región / Cuenta | Disponibilidad para Mox AI Chat |
| :-----------------------: | :-----------------------: | :-----------------------------: |
|            VPC            |             5             |                1                |
|           EIPs            |             5             |                1                |
|         S3 Bucket         |            100            |                4                |
|            EC2            |            32             |                2                |
|       RDS Instances       |            40             |                1                |
|       RDS Clusters        |            40             |                1                |
|     Lambda Functions      |           1000            |               14                |
|    API Gateway "APIs"     |            100            |                1                |
|    Cognito User Pools     |            60             |                1                |
| Application Load Balancer |            50             |                2                |
|        ECS Cluster        |          10,000           |                1                |

# 2.3 Recursos Clave
1. **Bucket para Estado de Instalación**: Mox AI Chat guarda el estado de la instalación en un bucket de Amazon S3. Este bucket debe ser creado previamente con un nombre predeterminado.
2. **Route 53 Hosted Zone**: aquí se gestionará el dominio o subdominio especificado para que Mox AI Chat opere. Una *hosted zone* será creada automáticamente si realizó la compra de dominio desde AWS.
3. **Certificado SSL**: para que el dominio que redirija a la solución de Mox AI Chat pueda funcionar correctamente, será necesaria la creación y aprobación de un certificado SSL.
4. **Modelos Bedrock:** el motor principal de la funcionalidad de IA Generativa de Mox AI Chat este servicio es usado tanto para procesar los documentos de entrada como para llevar un flujo conversacional con clientes cuando se necesite.

# 2.4 Actividad en Cuentas Nuevas de AWS
Para cuentas nuevas de AWS es necesario generar operaciones que demuestren que la cuenta está activa, este proceso es previo a la compra de dominios, para evitar el bloqueo en esta adquisición.

Para poder demostrar que la cuenta está activa, será necesario levantar un servidor, una instancia EC2, del tipo **t2.micro**. Esto deberá hacerse el suficiente tiempo para generar un gasto mínimo en la cuenta (apróx. 15 min).