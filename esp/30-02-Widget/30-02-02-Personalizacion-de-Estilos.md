El widget **ChatBot Go!** permite personalizar su apariencia mediante variables de CSS, facilitando la adaptación visual del componente a las necesidades de cada proyecto sin necesidad de modificar directamente el archivo CSS original. A continuación, se explica cómo utilizar estas variables para cambiar aspectos específicos del estilo del widget.

## Instrucciones de Personalización

Para personalizar el estilo del widget **ChatBot GO!**, defina las variables CSS en su propio archivo de estilos o directamente en el archivo HTML que incluya el componente. A continuación se detallan las variables disponibles y su función.

### Ejemplo de Implementación

A continuación, se muestra un ejemplo de cómo definir estas variables en un archivo CSS para cambiar la apariencia del widget:

```css
chat-bot {
    --chat-border-radius: 12px;
    --chat-background-color: #f9f9f9;
    --chat-width: 350px;
    --chat-height: 450px;
    --welcome-bubble-background: #ffcc00;
    --welcome-bubble-color: #333;
    --chat-header-background: linear-gradient(45deg, #ff6f61, #ff9966);
    --messages-background-color: #f5f5f5;
    --user-message-background: #ffe5d4;
    --bot-message-background: #e0f7fa;
    --button-background: #ff6f61;
}
```

### Descripción de Variables de Personalización

| Variable                          | Descripción                                                                                           | Valor Predeterminado         |
|-----------------------------------|-------------------------------------------------------------------------------------------------------|-------------------------------|
| `--chat-border-radius`            | Define el radio de los bordes del widget en modo expandido.                                           | `8px`                         |
| `--chat-background-color`         | Color de fondo del widget en modo expandido.                                                          | `transparent`                 |
| `--chat-width`                    | Ancho del widget en modo expandido.                                                                   | `300px`                       |
| `--chat-height`                   | Altura del widget en modo expandido.                                                                  | `400px`                       |
| `--chat-bottom-position`          | Posición desde la parte inferior de la pantalla.                                                      | `16px`                        |
| `--chat-right-position`           | Posición desde la parte derecha de la pantalla.                                                       | `16px`                        |
| `--welcome-bubble-background`     | Color de fondo de la burbuja de bienvenida.                                                           | `#007bff`                     |
| `--welcome-bubble-color`          | Color del texto de la burbuja de bienvenida.                                                          | `white`                       |
| `--welcome-bubble-padding`        | Espaciado interno de la burbuja de bienvenida.                                                        | `10px`                        |
| `--welcome-bubble-radius`         | Bordes redondeados de la burbuja de bienvenida.                                                       | `20px`                        |
| `--welcome-bubble-font-size`      | Tamaño de la fuente de la burbuja de bienvenida.                                                      | `14px`                        |
| `--chat-header-background`        | Color o degradado de fondo de la cabecera del chat en modo expandido.                                 | Degradado verde               |
| `--chat-header-color`             | Color del texto en la cabecera del chat.                                                              | `#fff`                        |
| `--chat-header-padding`           | Espaciado interno de la cabecera del chat.                                                            | `8px`                         |
| `--chat-header-radius`            | Bordes redondeados de la cabecera en modo expandido.                                                  | `8px 8px 0 0`                 |
| `--messages-padding`              | Espaciado interno del área de mensajes.                                                               | `24px`                        |
| `--messages-font-size`            | Tamaño de la fuente en los mensajes.                                                                  | `14px`                        |
| `--messages-background-color`     | Color de fondo del área de mensajes.                                                                  | `#ffffff`                     |
| `--messages-border`               | Borde del área de mensajes.                                                                           | `1px solid rgb(244, 242, 242)`|
| `--user-message-background`       | Color de fondo para los mensajes del usuario.                                                         | `#D4F1DE`                     |
| `--user-message-padding`          | Espaciado interno de los mensajes del usuario.                                                        | `10px`                        |
| `--user-message-radius`           | Bordes redondeados de los mensajes del usuario.                                                       | `10px`                        |
| `--bot-message-background`        | Color de fondo para los mensajes del bot.                                                             | `#E5E5EA`                     |
| `--bot-message-padding`           | Espaciado interno de los mensajes del bot.                                                            | `10px`                        |
| `--bot-message-radius`            | Bordes redondeados de los mensajes del bot.                                                           | `10px`                        |
| `--input-area-padding`            | Espaciado interno del área de entrada de texto.                                                       | `8px`                         |
| `--input-area-background`         | Color de fondo del área de entrada de texto.                                                          | `#ffffff`                     |
| `--input-area-border`             | Borde del área de entrada de texto.                                                                   | `1px solid rgb(244, 242, 242)`|
| `--button-background`             | Color de fondo del botón de envío.                                                                    | `#05ac3c`                     |
| `--button-color`                  | Color del texto del botón de envío.                                                                   | `#fff`                        |
| `--button-radius`                 | Bordes redondeados del botón de envío.                                                                | `4px`                         |
| `--link-color`                   | Color a los `<a>` que aparece en el mensaje                                                           | `#007BFF`|
### Aplicación de Estilos

Defina estas variables en el CSS de su proyecto para adaptar la apariencia del widget **ChatBot GO!**. El navegador aplicará estos valores sobre los estilos predeterminados, permitiendo una personalización visual completa sin modificar el código base del componente.

# Referencias
Lit Documentation. (n.d.). Using custom CSS properties in components. Recuperado de https://lit.dev/docs/components/styles/#customprops