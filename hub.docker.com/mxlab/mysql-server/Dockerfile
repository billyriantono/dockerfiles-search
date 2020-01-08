# Mysql server 

FROM mxlab/ubuntu-base
MAINTAINER Maxime Lacour <dockerhub@lacour-maxime.fr>

RUN apt-get update && \
    apt-get -y install mysql-server-5.5 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf

ADD run.sh /run.sh
RUN chmod +x /run.sh

VOLUME ["/var/lib/mysql"]

EXPOSE 3306

CMD ["/run.sh"]
