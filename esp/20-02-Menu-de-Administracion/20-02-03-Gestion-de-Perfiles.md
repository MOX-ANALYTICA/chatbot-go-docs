# 5.3.1 Descripción
Los perfiles de usuario son componentes que nos permiten controlar aspectos de la interacción de determinados usuarios con nuestra plataforma. Imaginemos el siguiente escenario, en nuestra empresa tenemos las áreas de ventas, finanzas y soporte. Además, tenemos documentos de ventas y manuales.
Para reflejar este comportamiento en el sistema, podemos hacer lo siguiente:
- creamos **colecciones** de documentos para ventas y manuales.
- creamos **perfiles** homólogos a las áreas de la empresa, y otorgamos el acceso a las colecciones deseadas.

Ahora, por medio de **asociaciones**, seremos capaces de asignar estos perfiles a los usuarios de distintas áreas. También configuramos el bot para asignarle un rol de soporte, un analista de finanzas o un asistente de ventas, todo esto dentro del mismo entorno de la aplicación.

![image](https://github.com/user-attachments/assets/2298dacb-af97-425d-a2ea-11c150dbdc08)

# 5.3.2 Atributos
Desde los componentes **perfiles** somos capaces de configurar:
1. **colecciones:** colecciones que a las que el perfil tendrá acceso (public, ventas, soporte, etc.).
2. **nro. documentos de búsqueda:** cantidad de documentos que serán consultados en cada pregunta del usuario (por defecto 4).
3. **nro. de mensajes del historial:** número par representativo de la cantidad de mensajes del historial a las que el bot tendrá acceso por cada pregunta (por defecto 50).
4. **prompt:** estructura de la información e instrucciones que utilizará el modelo por cada pregunta, se divide de la siguiente forma:
    1. **historial:** historial de mensajes de la conversación actual.
    2. **contexto:** información extraída de los documentos considerados "relevantes" para responder la pregunta del usuario.
    3. **system:** instrucciones directas al modelo (rol, nombre, reglas, ejemplos, consideraciones, etc.).
    4. **pregunta:** pregunta hecha por el usuario

# 5.3.3 Creación de Perfil