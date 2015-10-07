# IV-PLUCO-MFF
Proyecto PLUCO - Red Social PLUCO - Miguel Fernández Fernández

#INFRAESTRUCTURA VIRTUAL

#PLATAFORMA UNIVERSITARIA DE COMPARTICIÓN DE CONOCIMIENTOS: PLUCO

###Introducción

Plataforma académica de compartición de archivos de la Universidad de Granada, y que permita la colaboración en grupo entre los usuarios del sistema. Añade servicios de mensajería y foros,potenciando la interacción de los usuarios, y agrupando a los mismos por varios grupos de o bien asignaturas o cursos.

###Seguridad

En cuanto a la seguridad de nuestra plataforma los objetivos son: Permitir tener un sistema seguro en el que se separen datos sensibles y credenciales de los usuarios, y por otra parte archivos de los mismos. Por otra parte tendremos una web con foros que si es atacada no compremete la privacidad de los usuarios ni sus archivos.

###Infraestuctura

En mi infraestructura realizaré un sistema de almacenamiento sftp de recursos en la nube, que se usará para la organización, administración y compartición de archivos. Todo esto irá implementado en otro servidor que usaremos de Cloud Storage, además de un sistema de acceso a los datos y recursos por parte de los usuarios.
Tendremos al final un servicio de almacenamiento y compartición de recursos en la nube, donde cada usuario podrá subir sus propios archvivos y compartir archivos con los demás usuarios.
Tendremos que hacer un registro asociado a los usuarios que se dan de alta en la nube para permitir subir los mismos.
Para todo esto usaré un servidor Cloud Storage de Azure, y la web asociada a este servicio, y sus tablas de datos asociadas también.

El resto de mis compañeros deberán crear:

   1. Un sistema de gestión de datos de usuarios, mediante una base de datos que se gestionará por MySQL. Dicho sistema permitirá recuperar la información de los usuarios,consultar sus datos asociados. Además la gestión permitirá modificar los datos y los procesos asociados a dar de alta o baja de los usuarios.
   2. Un sistema web/red social de foros y dudas similar a Stackoverflow. Tendría detrás un servidor web para alojar las páginas y otro servidor para la base de datos de los usuarios.

Al final del proyecto, deberemos enlazar en conjunto las tres partes del proyecto, y realizar el despliegue correcto.
