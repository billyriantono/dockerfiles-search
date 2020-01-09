FROM ubuntu:16.04
MAINTAINER laraoa <laraoa@inta.es>
RUN apt-get -y update && apt-get install -y vim nginx
RUN rm -f /etc/nginx/sites-enabled/default
ADD index.html /var/www
ADD curso.conf /etc/nginx/conf.d/curso.conf
ENV domain=$domain
VOLUME /var/www
EXPOSE 80
CMD ["nginx", "-g",  "daemon off;"]
