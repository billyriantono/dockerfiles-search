FROM ubuntu:16.04
MAINTAINER William V. "william.al1979@gmail.com"
RUN apt-get update; apt-get install -y apache2 php libapache2-mod-php git
RUN sed -i 's_DocumentRoot /var/www/html_DocumentRoot /var/www/html/Loggin/_' /etc/apache2/sites-enabled/000-default.conf
RUN useradd -m -d /home/allex -s /bin/bash allex
SHELL ["/bin/bash", "-c"]
ENV APP=/var/www/html/
VOLUME ["/var/lib/docker/volumes/my-vol/_data"]
RUN mkdir /var/www/html/Loggin
COPY *.php /var/www/html/Loggin/
COPY assets/ /var/www/html/Loggin/
COPY class/ /var/www/html/Loggin/
LABEL version="1.0"
LABEL location="San Miguel El Salvador" type="Data Center" role="Web Server"
CMD ["/usr/sbin/apache2ctl","-D","FOREGROUND"]
EXPOSE 80
