FROM opensuse:latest
MAINTAINER "Virtual Apps <tovirtualapps@gmail.com>"
LABEL description="use this image to host your static web pages."

# install apache2 using zypper
RUN zypper -n update && zypper -n install apache2

# create welcome file for apache service
RUN echo "Welcome to virtualapps/opensuse-apache2, copy your web pages to /srv/www/htdocs/" > /srv/www/htdocs/index.html 

# start apache2 service
CMD ["apache2ctl", "-D FOREGROUND"]

