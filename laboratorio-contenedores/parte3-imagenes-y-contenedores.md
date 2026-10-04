````markdown
# Parte 3: Imágenes y contenedores

## Descarga de la imagen Ubuntu

Se ejecutó el siguiente comando:

```bash
docker pull ubuntu
```

El comando `docker pull` permite descargar una imagen desde un registro de imágenes de Docker. En este caso se descargó la imagen de Ubuntu.

## Consulta de imágenes disponibles

Posteriormente se ejecutó:

```bash
docker images
```

Este comando muestra las imágenes que se encuentran almacenadas localmente en el sistema.

### Evidencia

![Imágenes disponibles](imagenes/parte3-imagenes.png)

## Ejecución de un contenedor interactivo

Para crear un contenedor a partir de la imagen de Ubuntu y acceder a una terminal dentro de este se utilizó:

```bash
docker run -it ubuntu bash
```

La opción `-it` permite utilizar el contenedor de forma interactiva mediante una terminal.

Dentro del contenedor se ejecutaron los siguientes comandos:

```bash
ls
```

El comando `ls` permitió observar los archivos y directorios disponibles dentro del contenedor.

También se ejecutó:

```bash
pwd
```

Este comando mostró el directorio de trabajo actual dentro del contenedor.

Finalmente se utilizó:

```bash
cat /etc/os-release
```

Este comando permitió consultar información sobre el sistema Ubuntu disponible dentro del contenedor.

### Evidencia

![Contenedor Ubuntu](imagenes/parte3-ubuntu.png)

## Salida del contenedor

Para salir del contenedor se utilizó:

```bash
exit
```

Después de salir se ejecutó:

```bash
docker ps -a
```

El contenedor apareció en la lista, pero ya no se encontraba en ejecución.

### Evidencia

![Contenedores existentes](imagenes/parte3-contenedores.png)

## Preguntas de reflexión sobre imágenes y contenedores

### 1. ¿La imagen Ubuntu es lo mismo que una máquina virtual Ubuntu?

No. Una imagen de Docker contiene los archivos y componentes necesarios para crear contenedores, pero no representa una máquina virtual completa con su propio sistema operativo y kernel.

### 2. ¿Por qué el contenedor puede parecer un sistema Linux si no es una máquina virtual completa?

Porque el contenedor dispone de archivos, programas y herramientas propias del entorno Linux de la imagen utilizada, aunque no incluye un kernel independiente como una máquina virtual.

### 3. ¿Qué significa que el contenedor comparta el kernel con el host?

Significa que el contenedor utiliza el kernel proporcionado por el sistema anfitrión en lugar de ejecutar uno completamente independiente.

### 4. ¿Qué diferencia hay entre una imagen descargada y un contenedor creado?

Una imagen funciona como una plantilla que contiene los elementos necesarios para ejecutar una aplicación. Un contenedor es una instancia creada a partir de esa imagen que puede ejecutarse, detenerse y modific
