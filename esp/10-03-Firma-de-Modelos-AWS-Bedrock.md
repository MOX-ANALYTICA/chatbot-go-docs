# 10-03 Firma de Modelos AWS Bedrock
Para comenzar con la firma de modelos en Bedrock, siga estos pasos:
1. Ingrese a la cuenta AWS y acceda al servicio [Bedrock > Model Access](https://us-east-1.console.aws.amazon.com/bedrock/home?region=us-east-1#/modelaccess).
2. En la parte superior de la interfaz verá un botón amarillo "Enable model access".
3. Solicite acceso a los siguientes modelos específicos como se muestra en la captura:

<p align="center">
  <img src="https://github.com/MOX-ANALYTICA/chatbot-go-docs/blob/main/assets/10-03_1.png" />
</p>

4. Para los modelos Anthropic será necesario enviar un formulario, especifique los siguientes datos:
   - Nombre de la empresa (cliente)
   - Rubro
   - URL de su sitio web
   - Motivo de la solicitud: "We want to deploy a chatbot".

<p align="center">
  <img src="https://github.com/MOX-ANALYTICA/chatbot-go-docs/blob/main/assets/10-03_2.png" />
</p>

> **Nota**  
> - Si encuentra un error que impide la firma de los modelos seleccionados, es posible que se deba a que la cuenta es nueva y no tiene historial de gastos. En este caso, asegúrese de activar una instancia EC2 **t2.micro** durante 15 minutos y vuelva a intentarlo.
