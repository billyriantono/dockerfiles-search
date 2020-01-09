# docker run --rm -it --name wbd -v $PWD/conf:/etc/nginx/sites-enabled/ wbd
FROM ubuntu:16.04
RUN apt-get update && apt-get install nginx nginx-extras -y

COPY conf/webdav_conf /etc/nginx/sites-enabled/webdav_conf

VOLUME /etc/nginx/sites-enabled/
VOLUME /var/www

CMD nginx -g "daemon off;";