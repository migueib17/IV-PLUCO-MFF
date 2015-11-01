##Proyecto PLUCO - Red Social PLUCO

==

#INFRAESTRUCTURA VIRTUAL

# IV-PLUCO-MFF
Proyecto PLUCO - Red Social PLUCO - Miguel Fernández Fernández


[![Build Status](http://i1379.photobucket.com/albums/ah138/migueib17/7_zpshbawzozb.png)](http://i1379.photobucket.com/albums/ah138/migueib17/7_zpshbawzozb.png)


[![Shippable](http://i1379.photobucket.com/albums/ah138/migueib17/6_zps3vj8v1et.png)](http://i1379.photobucket.com/albums/ah138/migueib17/6_zps3vj8v1et.png)

[Apuntado en el proyecto de software libre de la oficina OSL](http://osl.ugr.es/bases-de-los-premios-a-proyectos-libres-de-la-ugr/)


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

==
#HITO 2 : Integracion Continua

##Configuracion

Para la configuración voy a usar un archivo makefile que generará los tests pertinentes, la documentación y por último ejecutará la aplicación.

```
#Makefile autor: Miguel Fernández Fernández
all: test doc run
clean:
rm -rf *~* && find . -name '*.pyc' -exec rm {} \;
rm -rf docs/*

test:
nosetests
doc:
pyccoon
run:
python _index_.py runserver 0.0.0.0:1111

```

Para la integración continua, voy a usar la herramienta Shippable, la cual es bastante fácil de usar y muy útil.
Para ello procedemos de la siguiente forma

1. Nos registramos en Shippable
2. Enlazamos con nuestro repositorio de github que queremos que tenga la integración continua.
3. Configuramos el archivo configuration.yml que es donde se pondrá las reglas que queremos que haga, los test, las herramientas a instalar etc.

##Pasos más detallados:

Para la integración y testeo de mi proyecto en github voy a usar [**Shippable**](https://app.shippable.com).
Para ello le damos a la opción de añadir un nuevo proyecto desde la interfaz web:
![Imagen](http://i1379.photobucket.com/albums/ah138/migueib17/1_zpsbpaf2woq.png)
Para la gestión y automatización de paquetes, usaré Pip de Python.
Para ello instalamos **python-pi** con el instalador de paquetes.

Nos creamos un archivo para hacer los test, con extensión **yml**:
```
language: python
build_image: shippableimages/ubuntu1204_python
python:
- 2.6
- 2.7
- 3.2
- 3.3
- 3.4
- pypy
author:
- Miguel Fdez Fdez
name:
- Pluco MFF
description:
- A platform for sharing information, with forums to sharing issues and resolve problems.
install:
- pip install pyyaml
- pip install grunt-django
- pip install nose
- pip install pytest
- pip install tox
- pip install pytest-cov
- pip install pytest-xdist
- easy_install nose
- pip install pystache
- pip install pygments
- pip install markdown
- pip install importlib
- pip install pyccoon

# Make folders for the reports
before_script:
- mkdir -p shippable/testresults
- mkdir -p shippable/codecoverage
- mkdir -p shippable/documentation
- mkdir -p shippable/test

script:
- which python
- nosetests
- pyccoon #generamos documentacion
- make   #ejecutamos makefile
#Basic test central
#- py.test --cov=tests/
#Distribution load test
#- py.test --cov= -n 2 tests/
notifications:
email:
- migueib17@correo.ugr.es

```

Subimos a github y esperamos a que se ejecuten las pruebas en shippable.
Se ejecuta correctamente:
![Shippable](http://i1379.photobucket.com/albums/ah138/migueib17/4_zpsyg0oevhg.png)
Los test funcionan correctamente en shippable
![TestShipable](http://i1379.photobucket.com/albums/ah138/migueib17/5_zpskc8cwq0c.png)

###Para los test he usado la herramienta NOSE
Es una herramiena para Python.

Código en python:
```
n = 10
nn= 20
def test_evens():

for i in range(0, 5):

yield check_even, i, i*3


def check_even(n, nn):
n = nn = 20
assert n % 2 == 0 or nn % 2 == 0
```
Como actualmente no tengo ninguna base de datos grande configurada, ni ningún fichero de proyecto simplemente he cogido un test de un programa aleatorio que no hace nada relacionado con mi proyecto. Simplemente es para comprobar que me funcionan los test y la integración continúa. Más adelante, en las próxima semana cambiaré este código por uno que comprueba por ejemplo el inicio de sesion de mis ususarios.

Subimos todo a git-hub para que travis detecte los cambios:
```
miguib17: ~/IV-PLUCO-MFF $ git push origin master
Username for 'https://github.com': migueib17
Password for 'https://migueib17@github.com':
Counting objects: 10, done.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 870 bytes | 0 bytes/s, done.
Total 6 (delta 2), reused 0 (delta 0)
To https://github.com/migueib17/IV-PLUCO-MFF
d6801b7..f1e2559  master -> master
```


##Integración Travis

He creado un archivo .travis.yml que contiene la configuración para otra parte de la integración continua en Shippable con travis:
```
language: python
build_image: shippableimages/ubuntu1204_python
python:
- 2.6
- 2.7
- 3.2
- 3.3
- 3.4
- pypy
author:
- MIGUEL FDEZ FDEZ
name:
- Pluco MFF
description:
- A platform for sharing information, with forums to sharing issues and resolve problems.
install:
- pip install pyyaml
- pip install grunt-django
- pip install nose
- pip install pytest
- pip install tox
- pip install pytest-cov
- pip install pytest-xdist
- easy_install nose
- pip install pystache
- pip install pygments
- pip install markdown
- pip install importlib
- pip install pyccoon

# Make folders for the reports
before_script:
- mkdir -p shippable/testresults
- mkdir -p shippable/codecoverage
- mkdir -p shippable/documentation
- mkdir -p shippable/test

script:
- which python
- nosetests
- pyccoon #generamos documentacion
- make   #ejecutamos makefile
#Basic test central
#- py.test --cov=tests/
#Distribution load test
#- py.test --cov= -n 2 tests/
notifications:
email:
- migueib17@correo.ugr.es

```
Es el mismo fichero que uso para shippable, ya que estoy haciendo lo mismo pero en 2 entornos de integración distintos.

Para que funcione todo en Travis, además de la configuraciónd de archivos, hace falta hacer como en shippable registrarse y enlazar reposotorio
1. Nos registramos [Travis](https://travis-ci.org)
2. Enlazamos repositorio ![img](http://i1379.photobucket.com/albums/ah138/migueib17/8_zpsgkt7chxc.png)
3. Subimos todo a git-hub para que travis detecte los cambios
```
migueib17: ~/IV-PLUCO-MFF $ git commit -m "Nuevo travis python"
[master 1342e2d] Nuevo travis python
1 file changed, 42 insertions(+), 28 deletions(-)
rewrite .travis.yml (72%)
rmigueib17: ~/IV-PLUCO-MFF $ git push origin master
```
4. Ejecutan los tests en Travis.
![Imagen Travis](http://i1379.photobucket.com/albums/ah138/migueib17/9_zpsinwhlwb6.png)