FROM ubuntu

RUN apt update && apt -y install apache2

COPY /src /var/www/html/

EXPOSE 80

CMD /usr/sbin/apache2ctl -D FOREGROUND
