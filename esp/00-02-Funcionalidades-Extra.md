Cualquier funcionalidad no contemplada en este documento **será considerado un proyecto y propuesta independiente** de esta aplicación. Algunos de los cambios requeridos más comunes, no contemplados en la aplicación base son los siguientes:
- Cambio, posición o tamaño de componentes UI
- Procesamiento de imágenes y/o información estructurada (tablas excel)
- Pre-procesamiento de documentos utilizados en la aplicación
- Acceso a fuentes de información alojadas en bases de datos
- Integración de la aplicación con CRMs externos
- Integración de la aplicación con plataformas como Teams, Zendesk, etc.

Consultar con el equipo de **Morris & Opazo** para la recepción de cualquier requerimiento adicional.

# 6.1 Modelo Gen AI y Consideraciones
- La interfaz de usuario es similar a la de las opciones comerciales más populares, ofreciendo una experiencia familiar en cuanto al manejo.
- Las respuestas se limitan al contenido cargado y conocimiento del modelo, el bot no cuenta con acceso a internet, por lo tanto las siguientes preguntas no serán respondidas correctamente:
  - ¿qué día es hoy?
  - ¿cuántas entradas hubieron el último mes?
  - ¿qué eventos relevantes ocurrieron este año?
- Actualmente el bot no se realiza un agregado de todos los documentos cargados, es decir, preguntas como las siguientes no serán respondidas correctamente:
  - ¿Cuántos documentos tienes?
  - Acabo de subir 10 boletas, por favor suma los montos.
  - ¿Cuáles son tus conocimientos?
  - Acabo de subir un libro de 4000 páginas, por favor resúmelo. (Esto no es posible porque, asumiendo que es un documento muy largo, se segmentará en diferentes partes.)

# 6.2 Procesamiento de Documentos
- La aplicación soporta exclusivamente documentos en formatos **.pdf, .docx** y **.txt** con contenido en texto plano.
- Las imágenes e información tabular incluida en los documentos no podrán ser procesados por el bot.
- Si un PDF contiene páginas escaneadas, serán interpretadas como imágenes y no podrán ser procesadas.
- El tiempo de procesamiento varía según el tamaño y complejidad del documento.
- No existe límite de carga de documentos, pero esto impactará en los costos asociados al uso de recursos en AWS y la velocidad de carga de estos en la interfaz visual.
- El peso máximo por cada documento es de **100MB** actualmente.
- Los documentos repetidos no son procesados ya que se verifica el contenido de estos previamente. No se toma en cuenta el nombre del archivo, es posible subir varios documentos con el mismo nombre pero de contenido distinto.
- Al eliminar un documento cargado, se borrarán tanto el archivo como demás referencias a él en distintas bases de datos que ChatBot Go! utiliza.

# 6.3 Consideraciones Adicionales
- Los servicios de ChatBot Go! no se encontrarán disponibles instantáneamente luego de un reinicio de estos, deberán pasar unos minutos antes de que pueda hacer uso de su aplicación.
- La velocidad de respuesta depende de varios factores y actualmente no es posible personalizar la ralentización o aceleración de estas.
- Los logos del cliente deben cumplir con especificaciones en cuanto a nombre y tipo de archivos **.png**, tal y como se detalla en la sección [Personalización de la WebApp](https://github.com/morrisopazo/chatbot-go-docs/wiki/4-Personalizaci%C3%B3n-de-la-WebApp).
