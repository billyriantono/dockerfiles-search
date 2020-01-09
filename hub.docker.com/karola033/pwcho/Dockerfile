FROM ubuntu
RUN apt-get update --yes; apt-get install --yes apache2

VOLUME /var/www/html
WORKDIR /var/www/html

EXPOSE 8080
CMD ["bash", "-c", "/etc/init.d/apache2 start; bash"]
