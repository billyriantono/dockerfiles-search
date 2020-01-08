FROM ubuntu:latest

RUN apt-get -y update; \
    apt-get -y install apache2; \
    service apache2 start;
ADD apache2.conf /etc/apache2/apache2.conf
EXPOSE 80
VOLUME /var/www/html
CMD ["bash"]
