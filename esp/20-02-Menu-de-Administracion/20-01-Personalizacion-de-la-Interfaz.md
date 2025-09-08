# 4.1 Imágenes por Defecto

ChatBot Go! se instala con un conjunto de imágenes predeterminadas que pertenecientes al propio producto. Estas imágenes están contenidas en un archivo comprimido denominado [go-media-custom.zip](https://mo-chat-go-artifacts-905418032146.s3.us-east-1.amazonaws.com/web-media-custom/go-web-custom.zip). Este archivo sirve como referencia para conocer el tamaño, nombre y extensión de las imágenes.

# 4.2 Pasos para Personalizar Imágenes y Colores
1. Descargue el archivo comprimido desde el siguiente link [go-media-custom.zip](https://mo-chat-go-artifacts-905418032146.s3.us-east-1.amazonaws.com/web-media-custom/go-web-custom.zip).
2. Descomprima el archivo en su equipo local para acceder a la estructura de referencia, aquí encontrará tanto archivos de imágenes **.png** como colores de la aplicación en formato **.css**. Consulte la siguiente estructura de archivos:
```
.
├── icon.png
└── static
    ├── css
    │   └── colours.css
    └── media
        ├── LogoCompany.png
        ├── LogoLogin.png
        └── iconchatcontainer.png

4 directories, 5 files
```

3. **Sustitución de Imágenes**: Sustituya las imágenes predeterminadas con las de su propia marca, asegurándose de mantener el mismo nombre, resolución y extensión de los archivos originales. Actualmente se recomienda contar con:
   - Un ícono con el logo de la empresa, sin fondo, formato **png**
   - Una imagen con el logo y nombre de la empresa, con fondo, formato **png**
   - Una imagen con el logo y nombre de la empresa, sin fondo, formato **png**

4. **Sustitución de Colores**: Dentro de la estructura del archivo descomprimido, diríjase a la ruta **/static/css/colours.css**, aquí reemplace los colores predeterminados por valores hexadecimales, siga la siguiente estructura:
```
.COLOUR_LOGIN_BACKGROUND_AND_LEFT_BAR {
  background-color: #1f2224;
}

.FOOTER_LEFT_BAR {
  background-color: #1f2224;
}

.BORDER_BUTTON_IN_LOGIN {
  border-color: #071d3b;
}


.BUTTON_IN_LOGIN {
  background-color: #071d3b  !important;
}

.BUTTON_IN_LOGIN:hover {
  background-color: #05162b !important;
}
```

# 4.3 Publicación de Marca Personalizada
Una vez que las imágenes y colores hayan sido personalizados a gusto, deberá subirlos a un bucket de AWS S3 específico, manteniendo la estructura de archivos y carpetas del zip. Siga estos pasos:

1. Diríjase al bucket nombrado como `chatbot-web-custom-ID_CUENTA`, donde `{ID_CUENTA}` es el identificador único de su cuenta.
2. Dentro de este bucket vacío arrastre el contenido de su carpeta ´web-media-custom´.
3. Finalmente, confirme la acción de subida y corrobore que las imágenes fueron actualizadas satisfactoriamente en la aplicación web.

> **Importante**  
> Es crucial que todos los archivos **mantengan el nombre** y formato **.png** originales para asegurar una integración sin problemas con la aplicación ChatBot Go!

![uploading-custom-media](https://github.com/morrisopazo/chatbot-go-docs/blob/main/assets/custom_media_uploading.gif)

4. Para asegurar que los recursos visuales se actualicen en el cache de CloudFront, será necesario ingresar a [Cloudfront > Distributions](https://us-east-1.console.aws.amazon.com/cloudfront/v4/home?region=us-east-1#/distributions), seleccionar la distribución de Chatbot Go! y crear un **invalidation** como se muestra a continuación.
<p align="center">
  <img src="https://github.com/morrisopazo/chatbot-go-docs/blob/main/assets/cdn_invalidation.png" />
</p>