# node_project



**Receta:** <https://www.digitalocean.com/community/tutorials/como-crear-una-aplicacion-node-js-con-docker-es>

## Requisitos previos

Para seguir este tutorial, necesitará lo siguiente:

- [Un servidor Ubuntu 18.04 configurado siguiendo las](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-18-04)
- [Docker instalado en su servidor, siguiendo los pasos 1 y 2 de ](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)
- [Node.js y npm instalados, siguiendo](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-18-04#installing-using-a-ppa)

En este tutorial, creará la imagen de una aplicación para un sitio web estático que utiliza el marco de trabajo Express y Bootstrap. Luego, creará un contenedor usando esa imagen y la insertará en Docker Hub para su uso futuro. Por último, extraerá la imagen almacenada de su repositorio de Docker Hub y creará otro contenedor para demostrar cómo puede recrear y escalar su aplicación.


## Paso 1: instalación de las dependencias de su aplicación

- Primero, cree un directorio para su proyecto en el directorio principal de su usuario no root. Llamaremos al nuestro [node_project], pero no es necesario que usted utilice la misma denominación.
  
- A continuación, cree un archivo [package.json] con las dependencias de su proyecto y otra información de identificación. 

- Añada la siguiente información sobre el proyecto, incluido su nombre, autor, licencia, punto de entrada y dependencias. Asegúrese de sustituir la información de autor con su propio nombre y sus detalles de contacto.

-Para instalar las dependencias de su proyecto, ejecute el siguiente comando:
- npm install
- Esto instalará los paquetes que haya incluido en su archivo package.json en el directorio de su proyecto.


## Paso 2: creación de los archivos de la aplicación

- Crearemos una página web que ofrece información a los usuarios sobre los tiburones. Nuestra aplicación tendrá un punto de entrada principal, app.js y un directorio views que incluirá los activos estáticos del proyecto. La página de inicio, [index.html], ofrecerá a los usuarios algunos datos preliminares y un enlace a una página con información más detallada sobre tiburones, [sharks.html]. En el directorio views, crearemos tanto la página de inicio como la página [sharks.html].

- Primero, abra el archivo [app.js] en el directorio principal del proyecto para definir las rutas del proyecto.

- La primera parte del archivo creará la aplicación Express y los objetos Router, y definirá el directorio base y el puerto como constantes: 
- path: define el directorio base, que será el subdirectorio de views dentro del directorio actual del proyecto.
- port: le indica a la aplicación que escuche el puerto 8080 y se conecte a él.

- A continuación, establezca las rutas de la aplicación usando el objeto router:
- La función router.use carga una función de middleware que registrará las solicitudes del router y las transmitirá a las rutas de la aplicación. Estas se definen en las funciones siguientes, que especifican que una solicitud GET a la URL del proyecto base debe devolver la página index.html, mientras que una solicitud GET a la ruta /sharks debe devolver sharks.html.

- A continuación, Comience por crear el directorio views:
- Abra el archivo de la página de destino, index.html.

- [Añada el siguiente código al archivo, que importará Bootstrap y creará un componente](https://getbootstrap.com/docs/4.0/components/jumbotron/) con un enlace a la página de información más detallada sharks.html

- Si siguió el tutorial de configuración inicial del servidor que se indica en los requisitos previos, tendrá un firewall activo que solo permite tráfico SSH. Para permitir el tráfico al puerto 8080 ejecute lo siguiente:
- [sudo ufw allow 8080]
- Ingrese la dirección http://your_server_ip:8080 en su navegador. Visualizará la siguiente página de destino.

## Paso 3: escribir el Dockerfile

- En este paso hay que crear dos ficheros que se llamaran Dockerfile y .dockerignore.
  
- Ahora vamos a crear  la imagen de la aplicación usando el comando docker build.Usar la marca -t con docker build le permitirá etiquetar la imagen con un nombre fácil de recordar. Dado que vamos a insertar la imagen en Docker Hub.

- La compilación de la imagen tomará entre uno y dos minutos. Una vez que se haya completado, verifique sus imágenes.


- Ahora, es posible crear un contenedor con esta imagen usandodocker run. Incluiremos tres marcas con este comando:
- -p
- -d
- --name
- Con el contenedor en ejecución, ahora, puede visitar su aplicación ingresando la dirección http://your_server_ip en su navegador. Visualizará la página de inicio de su aplicación una vez más.


## Paso 4: utilizar un repositorio para trabajar con imágenes

- Al insertar la imagen de su aplicación en un registro como Docker Hub, la pone a disposición para su uso posterior a medida que construye y escala sus contenedores. Demostraremos cómo funciona esto al insertar la imagen de la aplicación en un repositorio y, luego, usar la imagen para recrear nuestro contenedor.

