FROM 32bit/debian

RUN apt-get update && apt-get install -y apache2 libapache2-mod-php5
COPY script /usr/local/bin/

COPY web/ /var/www/html/

RUN chmod 777 /usr/local/bin/script

EXPOSE 80

CMD ["script"]