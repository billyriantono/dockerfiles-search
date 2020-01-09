FROM    debian:buster

LABEL	version="1.0"
LABEL	maintainer="casperklein"

RUN     apt-get update && apt-get install -y apache2

EXPOSE  80

CMD     apachectl start; tail -f /var/log/apache2/*
