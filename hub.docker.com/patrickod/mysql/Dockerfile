FROM paulczar/mysql
MAINTAINER Patrick O'Doherty <p@trickod.com>

RUN sed -i -e 's/127.0.0.1/0.0.0.0/' /etc/mysql/my.cnf
EXPOSE 3306

CMD ["sh", "-c", "mysqld"]
