FROM perl:latest

WORKDIR /app

RUN ls -la
RUN apt-get update
RUN apt-get install sendmail -y
RUN cpan Carton
RUN cpan Amon2
