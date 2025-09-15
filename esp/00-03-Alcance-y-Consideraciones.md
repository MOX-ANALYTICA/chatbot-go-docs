# 00-02 Alcance y Consideraciones
Cualquier funcionalidad no contemplada en este documento será considerada **un proyecto y propuesta independiente de esta aplicación**. Algunos de los cambios requeridos más comunes, no contemplados en la aplicación base, son los siguientes:

* Cambio, posición o tamaño de componentes UI.
* Procesamiento de imágenes y/o información estructurada (tablas de Excel).
* Pre-procesamiento de documentos utilizados en la aplicación.
* Acceso a fuentes de información alojadas en bases de datos.
* Integración de la aplicación con CRMs externos.
* Integración de la aplicación con plataformas como Teams, Zendesk, etc.

Para la recepción de cualquier requerimiento adicional, por favor, consulte con el equipo de **Morris & Opazo**.


## 1. Modelo de IA Generativa y Consideraciones
* La interfaz de usuario es similar a la de las opciones comerciales más populares, lo que ofrece una experiencia familiar en cuanto al manejo.
* Las respuestas se limitan al contenido cargado y al conocimiento del modelo. El bot **no cuenta con acceso a internet**, por lo tanto, las siguientes preguntas no serán respondidas correctamente:
    * ¿Qué día es hoy?
    * ¿Cuántas entradas hubo el último mes?
    * ¿Qué eventos relevantes ocurrieron este año?
* Actualmente, el bot no realiza un agregado de todos los documentos cargados. Preguntas como las siguientes no serán respondidas correctamente:
    * ¿Cuántos documentos tienes?
    * Acabo de subir 10 boletas, por favor suma los montos.
    * ¿Cuáles son tus conocimientos?
    * Acabo de subir un libro de 4000 páginas, por favor resúmelo. (Esto no es posible porque, asumiendo que es un documento muy largo, se segmentará en diferentes partes).

## 2. Procesamiento de Documentos
* La aplicación soporta exclusivamente documentos en formatos **.pdf**, **.docx** y **.txt** con contenido en texto plano.
* Las imágenes e información tabular incluida en los documentos no podrán ser procesadas por el bot.
* Si un PDF contiene páginas escaneadas, serán interpretadas como imágenes y no podrán ser procesadas.
* El tiempo de procesamiento varía según el tamaño y la complejidad del documento.
* No existe límite de carga de documentos, pero esto impactará en los costos asociados al uso de recursos en AWS y en la velocidad de carga en la interfaz visual.
* El peso máximo por cada documento es de **100 MB** actualmente.
* Los documentos repetidos no son procesados, ya que se verifica el contenido de estos previamente. No se toma en cuenta el nombre del archivo, por lo que es posible subir varios documentos con el mismo nombre, pero de contenido distinto.
* Al eliminar un documento cargado, se borrarán tanto el archivo como las demás referencias a él en las distintas bases de datos que Mox AI Chat utiliza.

## 3. Consideraciones Adicionales
* Los servicios de Mox AI Chat no estarán disponibles instantáneamente después de un reinicio. Deberán pasar unos minutos antes de que pueda hacer uso de la aplicación.
* La velocidad de respuesta depende de varios factores y, actualmente, no es posible personalizar la ralentización o aceleración de estas.
* Los logos del cliente deben cumplir con especificaciones en cuanto a nombre y tipo de archivo **.png**, tal como se detalla en la sección [Personalización de la Interfaz](10-04-Personalizacion-de-la-Interfaz.md).