````markdown
# Parte 5: Puertos, logs y variables de entorno

# Publicación de puertos

## Ejecución utilizando el puerto 5000

Se ejecutó la aplicación publicando el puerto 5000 mediante el siguiente comando:

```bash
docker run --name app-puertos -p 5000:5000 laboratorio-flask:1.0
```

La opción:

```text
-p 5000:5000
```

realiza un mapeo entre un puerto de la máquina anfitriona y un puerto del contenedor.

En este caso, el primer `5000` corresponde al puerto de la máquina anfitriona y el segundo `5000` corresponde al puerto utilizado por la aplicación dentro del contenedor.

La aplicación pudo accederse desde:

```text
http://localhost:5000
```

También se verificó la ruta:

```text
http://localhost:5000/info
```

### Evidencia

![Aplicación utilizando el puerto 5000](imagenes/parte5-puerto5000.png)

## Ejecución utilizando el puerto 8080

Posteriormente se ejecutó otro contenedor utilizando:

```bash
docker run --name app-puertos-2 -p 8080:5000 laboratorio-flask:1.0
```

En este caso, la aplicación continúa utilizando el puerto `5000` dentro del contenedor, pero se puede acceder a ella mediante el puerto `8080` de la máquina anfitriona.

La aplicación se abrió mediante:

```text
http://localhost:8080
```

### Evidencia

![Aplicación utilizando el puerto 8080](imagenes/parte5-puerto8080.png)

## Diferencia entre el puerto del host y el puerto del contenedor

El puerto del host corresponde al puerto utilizado en la máquina anfitriona para acceder al servicio.

El puerto del contenedor corresponde al puerto en el cual la aplicación escucha dentro del entorno del contenedor.

En la expresión:

```text
-p 8080:5000
```

el puerto `8080` pertenece al host y el puerto `5000` pertenece al contenedor.

## Preguntas de reflexión sobre puertos

### 1. ¿Por qué no basta con que la aplicación escuche en el puerto 5000 dentro del contenedor?

Porque el contenedor posee su propio entorno de red. Aunque la aplicación escuche en el puerto 5000 dentro del contenedor, es necesario publicar ese puerto para poder acceder a la aplicación desde la máquina anfitriona.

### 2. ¿Qué función cumple el mapeo de puertos?

El mapeo permite asoci