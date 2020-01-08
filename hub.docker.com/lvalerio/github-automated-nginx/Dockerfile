FROM fedora
MAINTAINER https://github.com/lvalerio

RUN dnf -y install nginx && dnf clean all
RUN dnf -y update && dnf clean all
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN echo "nginx on Fedora Container" > /usr/share/nginx/html/index.html

EXPOSE 80

CMD [ "/usr/sbin/nginx" ]
