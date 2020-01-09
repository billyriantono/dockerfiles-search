From ubuntu:14.04

# install apache
RUN apt-get update && DEBIAN_FRONTEND=nointeraction apt-get -y install \
         apache2 php5 libapache2-mod-php5

COPY index.html /var/www/html/

# run apache and expose port
EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND
