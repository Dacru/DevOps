
# 2. Implementación de un Pipeline CI/CD

Crear un pipeline de CI/CD para una aplicación Node.js basado en el siguiente repositorio: [frontend-challenge-base](https://github.com/sport-enlace-sas/frontend-challenge-base)




## Replicación del pipeline

1. En el archivo Jenkinsfile cambiar las credenciales de docker hub y kubernetes según las configuradas en el Jenkins.
2. En el jenkins instalar los plugines de docker pipeline y kubernetes y se pega el contenido del Jenkinsfile, asegurando de cambiar las URL de los repos, usuarios y credenciales.
3. Crear el pipeline en Jenkins para el registro en el docker hub.
4. Ejecutar el comando *kubectl apply -f k8s/application.yaml* para la configuración en el cluster.
5. Verificar los servicios con *kubectl get pods*.