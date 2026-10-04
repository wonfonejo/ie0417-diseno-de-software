# Laboratorio 2: Introducción práctica a contenedores con Docker

## IE0417 - Diseño de Software para Ingeniería

Este repositorio contiene el desarrollo del laboratorio de introducción práctica a contenedores con Docker.

Durante el laboratorio se trabajó con imágenes, contenedores, construcción de imágenes mediante Dockerfile, publicación de puertos, variables de entorno, volúmenes, bind mounts, redes y administración de recursos de Docker.

## Contenido del laboratorio

### Parte 1: Verificación de Docker

[Ver documentación](parte1-verificacion.md)

Se verificó la instalación y el funcionamiento de Docker mediante comandos como `docker --version`, `docker info` y `docker help`.

### Parte 2: Primer contenedor

[Ver documentación](parte2-comandos-basicos.md)

Se ejecutó el primer contenedor utilizando la imagen `hello-world` y se analizaron las diferencias entre contenedores activos y detenidos.

### Parte 3: Imágenes y contenedores

[Ver documentación](parte3-imagenes-y-contenedores.md)

Se descargó y utilizó la imagen de Ubuntu, se trabajó con contenedores interactivos y se practicaron operaciones de administración como iniciar, detener, acceder y eliminar contenedores.

### Parte 4: Aplicación Flask y Dockerfile

[Ver documentación](parte4-dockerfile.md)

Se creó una aplicación sencilla utilizando Flask y posteriormente se construyó una imagen personalizada mediante un Dockerfile.

El código de la aplicación se encuentra en:

```text
app/
├── Dockerfile
├── app.py
└── requirements.txt
```

### Parte 5: Puertos, logs y variables de entorno

[Ver documentación](parte5-puertos.md)

Se trabajó con publicación de puertos, consulta de logs, inspección de contenedores, estadísticas de recursos y configuración mediante variables de entorno.

### Parte 6: Volúmenes y bind mounts

[Ver documentación](parte6-volumenes.md)

Se utilizaron volúmenes de Docker para conservar información después de eliminar contenedores y bind mounts para utilizar archivos de la máquina anfitriona dentro de los contenedores.

### Parte 7: Redes de Docker

[Ver documentación](parte7-redes.md)

Se crearon redes personalizadas y se comprobó la comunicación entre diferentes contenedores utilizando Nginx y Redis.

### Parte 8: Limpieza del ambiente

[Ver documentación](parte8-limpieza.md)

Se revisaron y eliminaron recursos de Docker que ya no eran necesarios y se analizó el uso de espacio en disco.

# Reflexión final

## 1. ¿Qué es un contenedor?

Un contenedor es un entorno aislado en el que se puede ejecutar una aplicación junto con los archivos, dependencias y configuraciones que necesita. A diferencia de una máquina virtual completa, un contenedor utiliza recursos del sistema anfitrión y comparte su kernel.

## 2. ¿Qué problema resuelve Docker?

Docker facilita la creación de entornos consistentes para ejecutar aplicaciones. Permite empaquetar una aplicación junto con las dependencias necesarias, reduciendo problemas causados por diferencias entre las configuraciones de distintas computadoras.

## 3. ¿Qué diferencia hay entre una imagen y un contenedor?

Una imagen funciona como una plantilla que contiene los archivos y configuraciones necesarios para crear un entorno.

Un contenedor es una instancia creada a partir de una imagen que puede ejecutarse, detenerse, modificarse y eliminarse.

## 4. ¿Qué diferencia hay entre un contenedor y una máquina virtual?

Una máquina virtual incluye un sistema operativo completo y utiliza su propio kernel virtualizado.

Un contenedor es más ligero porque comparte el kernel con el sistema anfitrión y solamente incluye los componentes necesarios para ejecutar la aplicación.

## 5. ¿Qué aprendió sobre puertos?

Aprendí que una aplicación puede utilizar un puerto dentro del contenedor, pero para acceder a ella desde la máquina anfitriona es necesario publicar ese puerto.

También aprendí que no es necesario utilizar el mismo número de puerto en ambos lados. Por ejemplo:

```text
8080:5000
```

permite acceder mediante el puerto 8080 del host a una aplicación que utiliza el puerto 5000 dentro del contenedor.

## 6. ¿Qué aprendió sobre volúmenes?

Aprendí que los volúmenes permiten conservar información independientemente del ciclo de vida de los contenedores.

Un contenedor puede ser eliminado y otro contenedor puede utilizar posteriormente el mismo volumen para recuperar los datos almacenados.

También aprendí la diferencia entre un volumen administrado por Docker y un bind mount que utiliza directamente archivos o carpetas de la máquina anfitriona.

## 7. ¿Qué aprendió sobre redes?

Aprendí que Docker permite crear redes para que diferentes contenedores puedan comunicarse entre sí.

Los contenedores conectados a una misma red personalizada pueden utilizar sus nombres para encontrarse, lo que facilita la comunicación entre diferentes servicios de una aplicación.

## 8. ¿En qué casos usaría Docker en un proyecto de software?

Utilizaría Docker para crear un entorno reproducible de desarrollo y ejecución, especialmente en proyectos que dependen de versiones específicas de lenguajes, bibliotecas, bases de datos u otros servicios.

También puede ser útil cuando una aplicación está formada por diferentes servicios que necesitan ejecutarse de manera independiente.

## 9. ¿Qué parte del laboratorio le pareció más útil?

La parte relacionada con la construcción de una imagen mediante un Dockerfile me pareció especialmente útil porque permite definir de manera clara el entorno necesario para ejecutar una aplicación y posteriormente crear contenedores a partir de esa configuración.

También resultó útil observar cómo diferentes contenedores pueden comunicarse mediante redes de Docker.

## 10. ¿Qué parte le pareció más confusa?

Una de las partes que inicialmente resultó más confusa fue distinguir entre los diferentes mecanismos de almacenamiento y comprender la diferencia entre los datos internos de un contenedor, los volúmenes y los bind mounts.

Después de realizar las pruebas de persistencia fue más claro cómo cada mecanismo se utiliza para un propósito diferente.
