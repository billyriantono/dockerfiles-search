FROM hephaex/ubuntu
MAINTAINER Mario Cho <hephaex@gmail.com>

# Build essentials
RUN apt-get update && apt-get install -y nginx nginx-extras apache2-utils

VOLUME /media
EXPOSE 80
COPY webdav.conf /etc/nginx/conf.d/default.conf
RUN rm /etc/nginx/sites-enabled/*

COPY authorized.sh /
RUN chmod +x authorized.sh
CMD /authorized.sh && nginx -g "daemon off;"
