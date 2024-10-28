`DocProcessing` ofrece gestión de usuarios como una extensión. Para habilitar la gestión de usuarios, en tu archivo `flowsettings.py`, configura las siguientes variables:

- `KH_FEATURE_USER_MANAGEMENT`: True para habilitar.
- `KH_FEATURE_USER_MANAGEMENT_ADMIN`: el nombre de usuario del administrador. Este usuario se creará cuando la aplicación se inicie por primera vez.
- `KH_FEATURE_USER_MANAGEMENT_PASSWORD`: la contraseña del administrador. Este valor acompaña al nombre de usuario del administrador.

Una vez habilitado, tendrás acceso a las siguientes funciones:

- Inicio/cierre de sesión de usuario (ubicado en la pestaña de Configuración)
- Cambio de contraseña de usuario (ubicado en la pestaña de Configuración)
- Crear / Listar / Editar / Eliminar usuario (ubicado en Admin > Pestaña de Gestión de Usuarios)