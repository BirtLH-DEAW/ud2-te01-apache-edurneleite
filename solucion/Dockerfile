# Utiliza una imagen base de Ubuntu
FROM ubuntu:latest

# Actualiza los repositorios e instala Apache
RUN apt-get update && apt-get install -y apache2 && apt-get install nano

# Copia los archivos HTML al directorio de Apache
COPY www/ /var/www/

# Copia los certificados SSL al directorio correspondiente
COPY conf/certs/servidor.pem /etc/ssl/certs/servidor.pem
COPY conf/certs/servidor.key /etc/ssl/private/servidor.key

# Copia la configuración de Apache
COPY /conf/sites-available/ /etc/apache2/sites-available/

# Copia htpasswd
COPY /conf/htpasswd /etc/apache2/htpasswd

# Habilita el módulo SSL y el sitio SSL
RUN a2enmod ssl && a2ensite 000-default

# Exponer los puertos necesarios
EXPOSE 80 443

# Comando para iniciar Apache en segundo plano
CMD ["apachectl", "-D", "FOREGROUND"]
