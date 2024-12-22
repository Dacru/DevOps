
# 1. Diseño de Infraestructura

Diseñar una arquitectura para implementar una aplicación web escalable.




## Justificación técnica de la arquitectura propuesta

1. Se usa un balanceador de carga para que distribuya el tráfico de peticiones entre los diferentes clusteres con el fin de que haya alta disponibilidad.
2. La mayoría de los componentes están dockerizados, con el fin de ayudar a la portabilidad y escalibilidad del servicio, además de la sencilla configuración de los mismos.
3. Kubernetes será el encargado de administrar los contenedores ayudando a la escalibilidad, recuperación a fallos y despliegue automático.
4. En el pipeline se usa GitHub donde los desarrolladores harán los commits, luego jenkins detectará los cambions, compilará y ArgoCD desplegará los cambios en producción.
5. Referente al tema de alta disponibilidad en base de datos, se crean 2 nodos dockerizados de PostgreSQL en cluster usando Patroni o algún balanceador de carga, con replicación y configuración espejo y almacenamiento en AWS, GCP o Azure para el respaldo de la información.
6. Para el monitoreo se crean 2 contenedores, uno para el entorno de base de datos (Prometheus) y otro para el entorno gráfico (Grafana). Allí se realiza la configuración adecuada para la recolección de métricas de los distintos componentes de la arquitectura.