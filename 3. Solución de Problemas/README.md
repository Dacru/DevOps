
# 3. Solución de Problemas

Basado en el siguiente docker compose: [docker-compose.yaml](https://gist.github.com/DevOps-Inlaze/c8b21828cdda0bd12eb67e052211616b.j), corregir el archivo que está mal construído y optimizado.




## Errores Encontrados

1. No hay alguna directriz que evalue si los servicios estén respondiendo y funcionando de forma correcta.
2. En el archivo original, no hay política de reinicion automático para que se ejecute cuando los servicios fallen.
3. El servicio de Redis no tiene asignada red, por consiguiente no se podrá comunicar con alguno de los demás, generando problemas de conectividad. 
4. En un entorno de producción, el tema de puertosde Redis y postgres se podría omitir para que no sean expuestos, a menos que se requiera manejar tema de depuración. 
## Solución de errores y mejoras

1. Se configura la etiqueta healthcheck para que evalue cada uno de los servicios:

- Para el servicio de Nginx se hace una petición a http://localhost:80 a través de curl para comprobar el funcionamiento.
- Para el servicio de database se usa la función pg_isready para comprobar el estado de concetividad del servidor de DB.
- Para Redis se usa redis-cli para comprobar conexión y autnticación con el servicio.

2. Se agrega la política de reinicio *restart: always* para que los servicios se reinicien automáticamente por si llegasen a fallar.
3. En el servicio de Redis se define la misma red *app_network* que tienen los demás servicios para que puedan tener comunicación interna.
4. Se podría evitar colocar las credenciales en el fuente, y en su lugar crear un archivo .env creado en el mismo directorio donde está el compose para definirlas allí. Dicho alojaría algo como lo siguiente:

```
POSTGRES_USER=admin 
POSTGRES_PASSWORD=password123 
POSTGRES_DB=my_database 
REDIS_PASSWORD=redispass123
```

5. Se agrega el servicio de Redis como dependencia de app, siempre y cuando sean dependientes.
