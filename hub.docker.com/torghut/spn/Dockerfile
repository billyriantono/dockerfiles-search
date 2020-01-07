FROM debian:stretch

RUN apt-get update -y

RUN apt-get install -y apache2

RUN apt-get install -y php libapache2-mod-php

RUN apt-get install -y php-mysql

RUN apt-get install -y mysql-server

RUN apt-get install -y ansible

RUN apt-get install -y python-mysqldb

RUN apt-get install -y vim

RUN apt-get install -y net-tools

WORKDIR /var/www/html

COPY spn /var/www/html

COPY cmd.sh /

COPY setup.yaml /root

COPY ansible.cfg /root

COPY hosts /root

COPY spn.sql /root

RUN chmod +x /cmd.sh

ENTRYPOINT ["/cmd.sh"]
