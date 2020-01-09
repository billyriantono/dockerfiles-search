FROM ubuntu:latest

LABEL maintainer="Polec <mateusz.polec1@pollub.edu.pl>"

RUN apt-get update
RUN apt-get install -y apache2 && apt-get clean

EXPOSE 8080

CMD ["apachectl", "-D", "FOREGROUND"]
