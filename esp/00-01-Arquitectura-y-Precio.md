# 9.1 Arquitectura de la solución
![ARCHITECTURE drawio](https://github.com/user-attachments/assets/6bb9343f-0943-4c0f-a4c1-6b81334122eb)

# 9.2 Sobre el precio de la solución
El precio de esta solución se divide en costos **fijos** y **variables**:
- Los costos **fijos** se estiman en **$420** mensuales, estos dependen mayormente de las instancias EC2 y RDS utilizadas.
- Los costos **variables** se estiman entre $20 a $80 dependiendo del uso de los modelos GenAI, utilización del chatbot y documentos cargados.

# 9.3 Pausar la aplicación para ahorrar costos
Actualmente, ChatBot Go! no cuenta con una característica para pausar los servicios asociados de forma interactiva. Si usted aún desea pausar estos servicios, tendrá que hacerlo de forma manual, recuerde que esto es bajo su responsabilidad. A continuación se detallan los pasos:
> **Precaución**
> - El equipo de Morris & Opazo y el equipo de ChatBot Go! no recomiendan el apagado de estos servicios, menos aún si usted como cliente no está familiarizado con la consola AWS.
> - Morris & Opazo y el equipo de ChatBot Go! no se harán responsables por cualquier inconveniente que se presente debido a la manipulación de cualquier recurso asociado al proyecto de ChatBot Go!
> - La incorrecta manipulación de estos recursos podrían ocasionar la pérdida de información o falla permanente del bot, la reparación de estas fallas ocasionadas tendrá que ser coordinada con el equipo comercial de Morris, teniendo un costo adicional asociado.
> - Recuerde revertir estos cambios cuando desee poner en marcha nuevamente la aplicación, ya que esta no mostrará mayor información sobre los servicios no disponibles desde la interfaz web.

## 9.3.1 Pausar instancias EC2
1. Ingrese a su cuenta de AWS, verifique que se encuentra en la región **us-east-1**
2. diríjase al servicio de **EC2**
3. Seleccione la lista de instancias e identifique las instancias nombradas como **chat-**
4. También verifique que exista el tag **Project: Chatbot-GO** en estas instancias
![image](https://github.com/user-attachments/assets/964a3634-d364-4136-be42-f7000e9f7ffd)
5. Seleccione las instancias y presione el botón de **Actions > Stop instance** como se muestra a continuación
![image](https://github.com/user-attachments/assets/3ec37579-e4e4-40dd-9c92-c55b0ceb1ae7)
6. Esto dejará inoperativo el modelo generativo.

## 9.3.2 Pausar instancia RDS
1. Diríjase al servicio **RDS** en su cuenta AWS.
2. Luego seleccioné el menú **Databases** y observe el cluster nombrad **chat-aurora-vector**
3. Nuevamente, verifique los tags del recurso como se mostró en la anterior sección
4. Seleccione el cluster y haga clic en **Actions > Stop temporarily**, lea con detenimiento la pantalla de confirmación
5. Actualmente, el tiempo máximo de pausa será de 7 días, después el servicio de RDS se encontrará disponible nuevamente
![image](https://github.com/user-attachments/assets/983284f3-1f04-452d-a07c-282511389b55)

 