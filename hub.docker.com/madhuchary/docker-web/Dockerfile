FROM ubuntu:14.04
RUN apt-get update && apt-get install apache2 -y
EXPOSE 80
CMD apachectl  -f apache2.conf -DFOREGROUND
