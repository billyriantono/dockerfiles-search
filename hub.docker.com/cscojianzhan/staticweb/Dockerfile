FROM ubuntu:latest
MAINTAINER Docker Education Team <education@docker.com>

RUN apt-get update
RUN apt-get install -y nginx curl
RUN echo 'Hi, this is JZ2 web engine from jenkins' \
    >/var/www/html/index.html

COPY run_tests.sh /usr/local/bin/
RUN chmod 777 /usr/local/bin/run_tests.sh
CMD [ "nginx", "-g", "daemon off;" ]

EXPOSE 80
