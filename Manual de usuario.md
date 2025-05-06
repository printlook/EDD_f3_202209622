# Manual de Usuario - AutoGest Pro

## Índice
1. [Introducción](#introducción)
2. [Requerimientos del Sistema](#requerimientos-del-sistema)
3. [Instalación](#instalación)
4. [Inicio de Sesión](#inicio-de-sesión)
5. [Rol Administrador](#rol-administrador)
   - [Carga Masiva](#carga-masiva)
   - [Gestión de Usuarios](#gestión-de-usuarios)
   - [Gestión de Repuestos](#gestión-de-repuestos)
   - [Visualización de Logueo](#visualización-de-logueo)
   - [Generación de Servicios](#generación-de-servicios)
   - [Generación de Reportes](#generación-de-reportes)
   - [Gestión de Backup](#gestión-de-backup)
6. [Rol Usuario](#rol-usuario)
   - [Visualización de Vehículos](#visualización-de-vehículos)
   - [Visualización de Servicios](#visualización-de-servicios)
   - [Visualización de Facturas](#visualización-de-facturas)
7. [Resolución de Problemas](#resolución-de-problemas)
8. [Preguntas Frecuentes](#preguntas-frecuentes)

## Introducción

Bienvenido al manual de usuario de AutoGest Pro, un sistema integral de gestión diseñado específicamente para talleres de reparación de vehículos. Este software optimiza las operaciones diarias, desde el registro seguro de usuarios hasta la gestión de vehículos, repuestos, servicios y facturas, asegurando eficiencia y organización en todo momento.

AutoGest Pro incorpora estructuras avanzadas como grafo no dirigido, compresión Huffman, Blockchain y Árbol de Merkle, mejorando la seguridad, el análisis relacional y el almacenamiento de datos. La interfaz gráfica, desarrollada con GTK, ofrece un entorno intuitivo y adaptable para todos los usuarios.

![https://i.ibb.co/3Y99xCgH/Whats-App-Image-2025-05-06-at-4-11-55-PM.jpg]

## Requerimientos del Sistema

Para utilizar AutoGest Pro de manera óptima, asegúrese de que su sistema cumple con los siguientes requisitos:

- Sistema Operativo: Linux (cualquier distribución)
- Memoria RAM: 4GB o superior
- Espacio en disco: 500MB disponibles
- Resolución de pantalla recomendada: 1366x768 o superior
- Bibliotecas GTK+ instaladas

## Instalación

1. Descargue el paquete de instalación de AutoGest Pro desde el repositorio oficial
2. Abra una terminal en la ubicación donde descargó el archivo
3. Ejecute el comando de instalación:
   ```bash
   sudo ./instalar_autogest_pro.sh
   ```
4. Siga las instrucciones en pantalla para completar la instalación
5. Una vez finalizada la instalación, puede iniciar el programa ejecutando:
   ```bash
   autogest-pro
   ```



## Inicio de Sesión

Al iniciar AutoGest Pro, se presentará la pantalla de inicio de sesión donde puede acceder con sus credenciales:

1. Ingrese su correo electrónico en el campo "Correo"
2. Ingrese su contraseña en el campo "Contraseña"
3. Haga clic en el botón "Iniciar Sesión"

**Credenciales de Administrador:**
- Correo: admin@usac.com
- Contraseña: admin123

**Nota:** Si es la primera vez que utiliza el sistema, utilice las credenciales del administrador para comenzar a configurar el sistema.

![https://i.ibb.co/GvPnfSvc/Whats-App-Image-2025-05-06-at-4-12-35-PM.jpg]

## Rol Administrador

Como administrador del sistema, tendrá acceso a todas las funcionalidades de AutoGest Pro, incluyendo la gestión completa de usuarios, vehículos, repuestos, servicios y reportes.

![https://i.ibb.co/3Y99xCgH/Whats-App-Image-2025-05-06-at-4-11-55-PM.jpg]

### Carga Masiva

La funcionalidad de carga masiva permite importar múltiples registros de diferentes entidades en un solo proceso, ahorrando tiempo en la configuración inicial del sistema.

Para realizar una carga masiva:

1. Acceda al menú "Carga Masiva" en el panel de administrador
2. Seleccione "Cargar Archivos"
3. Navegue hasta la ubicación de los archivos JSON que contienen los datos a cargar
4. Seleccione los archivos correspondientes a las entidades que desea cargar (Usuarios, Vehículos, Repuestos, Servicios)
5. Haga clic en "Iniciar Carga"
6. Espere a que el sistema procese los archivos y muestre el resultado de la operación

![https://i.ibb.co/jvv72L3y/Whats-App-Image-2025-05-06-at-4-13-46-PM.jpg]

**Formato de los archivos JSON:**

- Usuarios:
```json
[
  {
    "ID": 1,
    "Nombres": "Carlos Alberto",
    "Apellidos": "Gomez Martinez",
    "Correo": "carlos.alberto@usac.com",
    "Edad": 20,
    "Contrasenia": "CarlosMartinez"
  }
]
```

- Vehículos:
```json
[
  {
    "ID": 1,
    "ID_Usuario": 1,
    "Marca": "Honda Civic",
    "Modelo": 2005,
    "Placa": "XZJ7H9K"
  }
]
```

- Repuestos:
```json
[
  {
    "ID": 1,
    "Repuesto": "Filtro de aceite",
    "Detalles": "Filtra impurezas del aceite del motor.",
    "Costo": 25.50
  }
]
```

### Gestión de Usuarios

#### Inserción de Usuarios

Para agregar un nuevo usuario al sistema:

1. Vaya a "Gestión de Usuarios" > "Nuevo Usuario"
2. Complete todos los campos requeridos:
   - ID
   - Nombres
   - Apellidos
   - Correo
   - Edad
   - Contraseña
3. Haga clic en "Guardar"

![https://i.ibb.co/4R9cG3YD/Whats-App-Image-2025-05-06-at-4-14-50-PM.jpg]

#### Visualización de Usuarios

Para consultar la información de un usuario específico:

1. Vaya a "Gestión de Usuarios" > "Consultar Usuario"
2. Ingrese el ID del usuario que desea visualizar
3. Haga clic en "Buscar"
4. Se mostrará la información del usuario solicitado



### Gestión de Repuestos

Para visualizar el inventario de repuestos disponibles en diferentes órdenes:

1. Vaya a "Gestión de Repuestos" > "Visualizar Repuestos"
2. Seleccione el tipo de recorrido que desea realizar:
   - PRE-ORDEN
   - IN-ORDEN
   - POST-ORDEN
3. Haga clic en "Generar Vista"
4. Se mostrará la lista de repuestos en el orden seleccionado



### Visualización de Logueo

Para monitorear la actividad de inicio y cierre de sesión de los usuarios:

1. Vaya a "Administración" > "Control de Logueo"
2. Seleccione el rango de fechas que desea consultar (opcional)
3. Haga clic en "Generar Reporte"
4. Se mostrará una tabla con la información de inicio y cierre de sesión de los usuarios



### Generación de Servicios

Para registrar un nuevo servicio en el sistema:

1. Vaya a "Servicios" > "Nuevo Servicio"
2. Complete los campos requeridos:
   - ID del Servicio
   - ID del Repuesto (debe existir en el sistema)
   - ID del Vehículo (debe existir en el sistema)
   - Detalles del servicio
   - Costo del servicio
3. Haga clic en "Registrar Servicio"

**Nota:** Al generar un servicio, automáticamente se creará una factura asociada y se establecerá una relación en el grafo no dirigido entre el vehículo y el repuesto utilizados.



### Generación de Reportes

Para generar reportes gráficos de las distintas entidades del sistema:

1. Vaya a "Reportes" > "Generar Reportes"
2. Seleccione el tipo de reporte que desea generar:
   - Usuarios
   - Vehículos
   - Repuestos
   - Servicios (recorrido IN-ORDEN)
   - Facturación
   - Grafo no dirigido
3. Haga clic en "Generar"
4. El sistema creará una imagen que se guardará en la carpeta "/Reportes"
5. Haga clic en "Visualizar" para ver el reporte generado



### Gestión de Backup

#### Generar Backup

Para crear una copia de seguridad de todas las entidades del sistema:

1. Vaya a "Administración" > "Backup" > "Generar Backup"
2. Haga clic en "Iniciar Proceso"
3. Espere a que el sistema genere los archivos de respaldo
4. Se notificará cuando el proceso haya finalizado correctamente

**Nota:** El sistema generará un archivo JSON para la entidad Usuarios (sin compresión) y archivos .edd comprimidos mediante el método Huffman para las entidades Vehículos y Repuestos.



#### Cargar Backup

Para restaurar el sistema a partir de copias de seguridad previas:

1. Vaya a "Administración" > "Backup" > "Cargar Backup"
2. Seleccione los archivos de backup que desea restaurar
3. Haga clic en "Iniciar Restauración"
4. El sistema validará la integridad de los archivos y cargará los datos
5. Se mostrará un mensaje de confirmación cuando el proceso haya finalizado

**Nota:** Si el sistema detecta corrupción en el Blockchain o discrepancias en los datos, mostrará un mensaje de error y no procederá con la carga.



## Rol Usuario

Como usuario regular del sistema, tendrá acceso a las funcionalidades relacionadas con sus propios vehículos, servicios y facturas.



### Visualización de Vehículos

Para consultar los vehículos registrados a su nombre:

1. Vaya a "Mis Vehículos" en el menú principal
2. Se mostrará una lista con todos los vehículos asociados a su cuenta
3. Puede hacer clic en cualquier vehículo para ver sus detalles completos



### Visualización de Servicios

Para consultar los servicios realizados a sus vehículos:

1. Vaya a "Mis Servicios" en el menú principal
2. Seleccione el tipo de recorrido para visualizar los servicios:
   - PRE-ORDEN
   - IN-ORDEN
   - POST-ORDEN
3. Haga clic en "Aplicar Filtro"
4. Se mostrará la lista de servicios en el orden seleccionado



### Visualización de Facturas

Para consultar las facturas pendientes de pago:

1. Vaya a "Mis Facturas" en el menú principal
2. Se mostrará una tabla con todas las facturas asociadas a sus servicios
3. Puede ordenar las facturas por fecha, monto o estado de pago
4. Para ver los detalles de una factura específica, haga clic en el número de factura



## Resolución de Problemas

### El sistema no inicia correctamente

- Verifique que cumple con los requisitos mínimos del sistema
- Asegúrese de que las bibliotecas GTK+ están correctamente instaladas
- Compruebe los permisos de los archivos ejecutables

### Error en la carga masiva

- Verifique que el formato de los archivos JSON es correcto
- Asegúrese de que no existen IDs duplicados en los registros
- Compruebe las relaciones entre entidades (por ejemplo, que el ID_Usuario de un vehículo existe en la entidad Usuarios)

### No se pueden generar reportes gráficos

- Verifique que Graphviz está correctamente instalado en su sistema
- Asegúrese de que la carpeta "/Reportes" existe y tiene permisos de escritura
- Compruebe si hay suficiente espacio en disco

## Preguntas Frecuentes

### ¿Cómo puedo cambiar mi contraseña?

Para cambiar su contraseña:
1. Inicie sesión en el sistema
2. Vaya a "Mi Perfil" > "Cambiar Contraseña"
3. Ingrese su contraseña actual y la nueva contraseña
4. Haga clic en "Guardar Cambios"

### ¿Puedo exportar los reportes a otros formatos?

Actualmente, los reportes se generan en formato de imagen utilizando Graphviz. Para convertirlos a otros formatos, deberá utilizar herramientas externas de conversión de imágenes.

### ¿Qué hacer si olvidé mi contraseña?

Si olvidó su contraseña, contacte al administrador del sistema para que restablezca sus credenciales de acceso.

### ¿Cómo puedo registrar un nuevo vehículo?

Como usuario regular, no puede registrar vehículos directamente. Debe solicitar al administrador que registre el vehículo asociado a su cuenta.

---

Para más información o soporte técnico, contacte al equipo de desarrollo a través del correo electrónico: soporte@autogestpro.com
