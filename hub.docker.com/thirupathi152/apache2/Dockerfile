FROM centos:latest as builder

MAINTAINER NewstarCorporation

RUN yum install -y httpd

COPY index.html /var/www/html/
EXPOSE 80
ENTRYPOINT ["/usr/sbin/apachectl", "-D", "FOREGROUND"]

#FROM nginx as stage2
#COPY --from=builder /var/www/html /usr/share/nginx/html
