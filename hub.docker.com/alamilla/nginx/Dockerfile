# nginx
#
# VERSION               1.0

FROM     alamilla/base
MAINTAINER Andres F. Lamilla, "alamilla@gmail.com"

# se actualiza la base de datos de apt
RUN apt-get update -qq

# instalacion de los paquetes necesarios para la app
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y nginx

# se adicionan los archivos template de configuracion
ADD src/nginx.sv.conf /etc/supervisor/conf.d/nginx.sv.conf
ADD src/run.sh /usr/local/bin/run.sh
ADD src/start_nginx.sh /usr/local/bin/start_nginx.sh
RUN chmod +x /usr/local/bin/*.sh

# Se elimina la pagina por defecto
RUN rm /etc/nginx/sites-enabled/*

# Se adiciona la configuracion de nginx
ADD src/static_content /etc/nginx/sites-enabled/static_content
ADD src/noversion.conf /etc/nginx/conf.d/noversion.conf

# se crea el enlace al nuevo directorio de arhivos web
RUN mkdir /app
RUN rm -rf /usr/share/nginx/html
RUN ln -s /app /usr/share/nginx/html

EXPOSE 80
CMD ["/usr/local/bin/run.sh"]
