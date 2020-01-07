# Version: 0.0.1
FROM ubuntu:16.04
MAINTAINER Brian Collins "rbc@rbcollins.net"
RUN apt-get update; apt-get install -y nginx
RUN echo 'Some container' > /var/www/html/index.html
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["-h"]
