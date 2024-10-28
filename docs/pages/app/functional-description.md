## Gestión de grupos de usuarios/inquilinos

### Crear nuevo grupo de usuarios

(6 días-hombre)

**Descripción** : cada cliente tiene un grupo de usuarios dedicado. Cada grupo de usuarios tiene un
Usuario administrador que puede realizar tareas administrativas (por ejemplo, crear una cuenta de usuario en esa
grupo de usuarios...). El flujo de trabajo para crear un nuevo grupo de usuarios es el siguiente:

1. Accede a la interfaz de administración de grupos de usuarios.
2. En el panel “Crear grupo de usuarios” proporcionamos:
a. Nombre del cliente: p. ej. Apple.
b. Nombre de subdominio: p. ej. apple.
c. Correo electrónico de administrador, nombre de usuario y contraseña.
3. El sistema:
a. Una implementación de la plataforma Aurora con el subdominio especificado.
b. Envíe un correo electrónico al administrador, con el nombre de usuario y la contraseña.

**Expectativa** :

- El administrador puede ir a la plataforma Aurora implementada.
- El administrador puede iniciar sesión con el nombre de usuario y la contraseña especificados.

**Condición** :

- Cuando el nombre de subdominio ya existe, se genera un error.
- Si se produce un error al enviar el correo electrónico al cliente, genere el error y elimine el correo electrónico.
grupo de usuarios recién creado.
- Regla de contraseña:
- Tener al menos 8 caracteres.
- Debe contener mayúsculas, minúsculas, números y símbolos.

---

### Eliminar grupo de usuarios

(2 días-hombre)

**Descripción** : en la página de administración de inquilinos, podemos eliminar el usuario seleccionado
grupo. El flujo de usuario es el siguiente:

1. Accede a la interfaz de administración de grupos de usuarios,
2. Ver la lista de grupos de usuarios.
3. Junto al grupo de usuarios de destino, haga clic en eliminar.
4. Confirme si desea eliminar.
5. En caso afirmativo, elimine el grupo de usuarios. En caso negativo, cancele la operación.

**Expectativa** : cuando se elimina un grupo de usuarios, esperamos eliminar todo
relacionado con los grupos de usuarios: dominio, archivos, bases de datos, cachés, implementaciones.

## Gestión de usuarios

---

### Crear cuenta de usuario (para usuario administrador)

(1 día-hombre)

**Descripción** : el usuario administrador en la cuenta del cliente puede crear una cuenta de usuario
Para ese grupo de usuarios, para crear el nuevo usuario, el administrador del cliente debe hacer lo siguiente:

1. Vaya a "Administrador" > "Usuarios"
2. En el panel "Crear usuario", proporcione:
- Nombre de usuario
- Contraseña
- Confirmar Contraseña
3. Haga clic en "Crear"

**Expectativa** :

- El usuario puede crear la cuenta.
- El nombre de usuario:
- No distingue entre mayúsculas y minúsculas (por ejemplo, Moon y moon serán lo mismo)
- Solo puede contener estos caracteres: az AZ 0-9 \_ + - .
- Tiene una longitud máxima de 32 caracteres.
- La contraseña está sujeta a la siguiente regla:
- Longitud mínima de 8 caracteres
- Contiene al menos 1 número
- Contiene al menos 1 letra minúscula
- Contiene al menos 1 letra mayúscula
- Contiene al menos 1 carácter especial del siguiente conjunto, o un
carácter de espacio no inicial ni final: `^ $ * . [ ] { } ( ) ? - " ! @ # % & / \ , > < ' : ; | _ ~ ` + =

---

### Eliminar cuenta de usuario (para usuario administrador)

**Descripción** : el usuario administrador en la cuenta del cliente puede eliminar la cuenta de usuario.
Una vez que se elimina una cuenta de usuario, éste no podrá iniciar sesión en la Plataforma Aurora.

1. El usuario administrador navega a "Administrador" > "Usuarios".
2. En el panel de lista de usuarios, junto al nombre de usuario, el administrador hace clic en "Eliminar".
Botón. Aparece el cuadro de diálogo de confirmación.
3. Si selecciona "Eliminar", se elimina la cuenta de usuario. Si selecciona "Cancelar", no haga nada.
El diálogo de confirmación desaparece.

**Expectativa** :

- Una vez eliminado el usuario, se eliminará la siguiente información relativa al usuario:
ser eliminado:
- Su entorno personal.
- Sus conversaciones.
- Se conservarán los siguientes datos relativos al usuario:
- Sus archivos cargados.

---

### Editar cuenta de usuario (para usuario administrador)

**Descripción** : el usuario administrador puede cambiar cualquier información sobre el usuario.
Cuenta, incluida la contraseña. Para cambiar la información del usuario:

1. El usuario administrador navega a "Administrador" > "Usuarios".
2. En el panel de lista de usuarios, junto al nombre de usuario, el administrador hace clic en "Editar".
botón.
3. La lista de usuarios desaparece, aparece el detalle del usuario, con lo siguiente
La información aparece:
- Nombre de usuario: (rellene previamente el nombre de usuario)
- Contraseña: (en blanco)
- Confirmar contraseña: (en blanco)
4. El administrador puede editar cualquier información y hacer clic en "Guardar" o "Cancelar".
- Si "Guardar": la información se actualizará en la base de datos, o se mostrará
Error según expectativa a continuación.
- Si "Cancelar": omitir.
5. Si se guarda correctamente o se cancela, se transfiere nuevamente a la interfaz de usuario de la lista de usuarios, donde se encuentra el usuario.
La información se actualiza en consecuencia.

**Expectativa** :

- Si la "Contraseña" y "Confirmar contraseña" son diferentes entre sí, mostrar
Error: "La contraseña no coincide".
- Si tanto "Contraseña" como \*"Confirmar contraseña" están en blanco, no cambie el usuario
contraseña.
- Si se cambia la contraseña, la regla de contraseña está sujeta a la misma regla cuando
creando usuario.
- Es posible cambiar el nombre de usuario. Si se cambia el nombre de usuario, el usuario de destino debe
Utilice el nuevo nombre de usuario.

---

### Iniciar sesión

(3 días-hombre)

**Descripción** : los usuarios pueden iniciar sesión en la Plataforma Aurora de la siguiente manera:

1. El usuario navega a la URL.
2. Si el usuario no ha iniciado sesión, la interfaz de usuario solo muestra la pantalla de inicio de sesión.
3. El usuario escribe su nombre de usuario y contraseña.
4. Si es correcto, el usuario pasará a la interfaz de usuario de funcionamiento normal.
5. Si es incorrecto, la pantalla de inicio de sesión muestra un error de texto.

---

### Desconectar

(1 día-hombre)

**Descripción** : el usuario puede cerrar sesión en la Plataforma Aurora de la siguiente manera:

1. El usuario navega a la página Configuración > Usuario.
2. El usuario hace clic en cerrar sesión.
3. El usuario cierra la sesión en la pantalla de inicio de sesión de la interfaz de usuario.

**Expectativa** : el usuario cierra la sesión por completo. La próxima vez que utilice el
Plataforma Aurora, debe iniciar sesión nuevamente.

---

### Cambiar la contraseña

**Descripción** : el usuario puede cambiar su contraseña de la siguiente manera:

1. El usuario navega a la página Configuración > Usuario.
2. En la sección de cambio de contraseña, el usuario proporciona esta información y hace clic
Cambiar:
- Contraseña actual
- Nueva contraseña
- Confirmar nueva contraseña
3. Si el cambio se realizó correctamente, se cambiará la contraseña. De lo contrario, se mostrará la
Error en la interfaz de usuario.

**Expectativa** :

- Si el cambio de contraseña se realiza correctamente, la próxima vez que cierren sesión o inicien sesión en el sistema,
Puede utilizar la nueva contraseña.
- Regla de contraseña (la misma que la regla de contraseña normal al crear un usuario)
- Errores:
- La contraseña no coincide.
- Se violaron las reglas de contraseña.

---

## Charlar

### Chatea con el bot

**Descripción** : La Plataforma Aurora se centra en preguntas y respuestas sobre el tema.
Datos cargados. Cada chat tiene los siguientes componentes:

- Mensaje de chat: muestra el intercambio entre bots y humanos.
- Entrada de texto + botón de envío: para que el usuario ingrese el mensaje.
- Panel de origen de datos: para seleccionar los archivos que delimitarán el contexto para el
bot.
- Panel de información: muestra evidencia mientras el bot responde las preguntas del usuario.

El flujo de trabajo del chat se ve así:

1. [Opcional] El usuario selecciona los archivos que desea que formen parte del contexto del bot.
Si el usuario no selecciona ningún archivo, se seleccionarán todos los archivos en la Plataforma Aurora.
sea el contexto para el bot.
- El usuario puede escribir mensajes de varias líneas, utilizando "Shift + Enter" para
salto de línea.
2. El usuario envía el mensaje (haciendo clic en el botón Enviar o presionando Enter).
llave).
3. El bot en la conversación de chat devolverá "Pensando..." mientras
procesos.
4. El panel de información de la derecha comienza a mostrar datos relacionados con el usuario.
mensaje.
5. El robot comienza a generar una respuesta. El marcador de posición "Pensando..." desaparece.

** Expectativa ** :

- Mensajes:
- El usuario puede enviar mensajes de varias líneas, utilizando "Shift + Enter" para saltar una línea.
- El usuario puede indicar que le gusta o no a la respuesta de la IA. Esta información es
registrado en la base de datos.
- El usuario puede hacer clic en el botón de copia en el mensaje de chat para copiar el contenido a
portapapeles.
- Panel informativo:
- El panel informativo muestra la evidencia más reciente.
- El usuario puede hacer clic en el mensaje y aparecerá la referencia a ese mensaje.
Aparece en el "Panel de referencia" (función en planificación).
- El usuario puede hacer clic en el título para mostrar/ocultar el contenido.
- Todo el panel de información se puede contraer.
- Calidad del chatbot:
- El usuario puede conversar con el bot. El bot responde las solicitudes del usuario de una manera
manera natural.
- El mensaje del bot debe transmitirse a la interfaz de usuario. El bot no espera a recopilar
    toda la respuesta de texto y luego vuelca todas a la vez.

### Conversación - cambiar

**Descripción** : los usuarios pueden saltar entre diferentes conversaciones. Pueden
Ver la lista de todas las conversaciones, puede seleccionar una conversación antigua y continuar.
El chat en el contexto de la conversación anterior. El flujo de trabajo de cambio es
como esto:

1. Los usuarios hacen clic en el menú desplegable de conversaciones. Se mostrará una lista de
conversaciones.
2. Dentro de ese menú desplegable, el usuario selecciona una conversación.
3. Los mensajes de chat, el panel de información y los datos seleccionados mostrarán el contenido.
en ese viejo chat.
4. El usuario puede continuar chateando normalmente en el contexto de este chat antiguo.

**Expectativa** :

- En la lista desplegable de conversaciones, las conversaciones se ordenan en creadas.
orden de fecha.
- Cuando no hay conversación, la lista de conversaciones está vacía.
- Cuando no hay conversación, el usuario aún puede conversar con el bot de chat.
Al hacerlo, se crea automáticamente una nueva conversación.

### Conversación - crear

**Descripción** : el usuario puede iniciar explícitamente una nueva conversación con el
robot conversacional:

1. El usuario hace clic en el botón "Nuevo".
2. La nueva conversación se crea automáticamente.

**Expectativa** :

- El nombre de la conversación predeterminada es la fecha y hora actual.
- Quedó seleccionado.
-Se agrega a la lista de conversaciones.

### Conversación - cambiar nombre

**Descripción** : el usuario puede cambiar el nombre del chatbot escribiendo el nombre y haciendo clic en
el botón Cambiar nombre que se encuentra al lado.

- Si el cambio de nombre se realiza correctamente: el nombre que se muestra en el primer menú desplegable cambiará en consecuencia
- Si el cambio de nombre no se realiza correctamente: muestra un mensaje de error en color rojo debajo de la sección de cambio de nombre

**Condición** :

- Restricción de nombre:
- Min. caracteres: 1
- Máximo de caracteres: 40
- No se pudo tener el mismo nombre con una conversación existente del mismo nombre.
usuario.

### Conversación - eliminar

**Descripción** : el usuario puede eliminar la conversación existente de la siguiente manera:

1. Haga clic en el botón Eliminar.
2. La interfaz de usuario muestra confirmación con 2 botones:
- Borrar
- Cancelar.
3. Si desea eliminar, elimine la conversación y pase a la siguiente conversación más antigua.
cerrar el panel de confirmación.
4. Si cancela, simplemente cierre el panel de confirmación.

## Gestión de archivos

La gestión de archivos permite a los usuarios cargar, enumerar y eliminar archivos que deseen.
subir a la Plataforma Aurora

### Subir archivo

**Descripción** : el usuario puede cargar archivos a la Plataforma Aurora. Los archivos cargados
Los archivos se utilizarán como contexto para que nuestro chatbot haga referencia a ellos cuando converse.
con el usuario. Para cargar un archivo, el usuario:

1. Vaya a la pestaña Archivo.
2. Dentro de la pestaña Archivo, hay una sección Cargar.
3. El usuario puede agregar archivos a la sección Cargar mediante arrastrar y soltar, o haciendo clic.
en el explorador de archivos.
4. El usuario puede seleccionar algunas opciones relacionadas con la carga y la indexación. Dependiendo de
El proyecto, estas opciones pueden ser diferentes. Sin embargo, se discutirán
abajo.
5. El usuario hace clic en el botón "Cargar e indexar".
6. La aplicación muestra notificaciones cuando comienza y finaliza la indexación y cuando se producen errores.
sucede en la esquina superior derecha.

**Opciones** :

- Forzar la reindexación de archivos. Cuando el usuario intenta cargar archivos que ya existen en
El sistema:
- Si esta opción es Verdadera: volverá a indexar esos archivos.
- Si esta opción es Falso: omitirá la indexación de esos archivos.

**Condición** :

- Número máximo de archivos: 100 archivos.
- Número máximo de páginas por archivo: 500 páginas
- Tamaño máximo de archivo: 10 MB

### Listar todos los archivos

**Descripción** : el usuario puede saber qué archivos están en el sistema mediante:

1. Vaya a la pestaña Archivo.
2. De forma predeterminada, se mostrarán todos los archivos cargados, cada uno con lo siguiente:
Información: nombre del archivo, tamaño del archivo, número de páginas, fecha de carga
3. La interfaz de usuario también muestra el número total de páginas y el número total de tamaños en MB.

### Eliminar archivo

**Descripción** : los usuarios pueden eliminar archivos de esta interfaz de usuario para liberar espacio o
Eliminar información obsoleta. Para eliminar los archivos:

1. El usuario navega a la pestaña Archivo.
2. En la lista de archivos, al lado de cada archivo, hay un botón Eliminar.
3. El usuario hace clic en el botón Eliminar. Aparece un cuadro de diálogo de confirmación.
4. Si selecciona Eliminar, elimine el archivo. Si selecciona Cancelar, cierre el cuadro de diálogo de confirmación.

**Expectativa** : una vez eliminado el archivo:

- Se elimina la entrada de la base de datos de ese archivo.
- El archivo se elimina de "Chat - Fuente de datos".
- El número total de páginas y el tamaño de MB se reducen en consecuencia.
- Se mantiene la referencia al expediente en el panel informativo.
