FROM blitznote/debootstrap-amd64:16.10
RUN apt-get update
RUN apt-get -y install apache2
EXPOSE 80
CMD ["/usr/sbin/apache2ctl"] -D FOREGROUND

