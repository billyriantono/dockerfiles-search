FROM ubuntu:16.04
RUN apt-get update
RUN apt install -y vim nginx
RUN rm -f /etc/nginx/sites-enabled/default
ADD index.html /var/www
ADD curso.conf /etc/nginx/conf.d/curso.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

