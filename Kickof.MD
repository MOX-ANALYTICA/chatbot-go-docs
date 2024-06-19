Requisitos Solicitados en el Kick Off
Requisitos necesarios para poder empezar con la implementación, esta sección contempla input necesarios del cliente, así como requisitos fundamentales para poder implementar la solución
1. Apertura de cuenta del cliente en AWS y acceso a usuario de Morris&Opazo mediante AWS Organizations y CloudFormation.
2. Política de permisos personalizada que se asignará al usuario de Morris en la cuenta del cliente, con acceso limitado a determinados servicios (Cognito, Route53, EC2, ECS, CloudFront, Bedrock, etc.)
   
   Nota:Generar política personalizada para configurar en la cuenta de AWS, evitar full admin.

3.En caso de que MO tenga que gestionar la compra del dominio  
    Información sobre los datos personales del cliente para la compra del dominio en Route 53, se requiere información de:

   Nombre y Apellido del representante

   Email

   Numero de telefono con el codigo de pais (+51, +53, +56, etc)

   País

   Ciudad
   Dirección
   Código Postal Zip
   URL de sitio web (firma de modelos Bedrock)
   Documentos con información del cliente en formato pdf para poder alimentar la base de conocimiento de Chatbot GO!
