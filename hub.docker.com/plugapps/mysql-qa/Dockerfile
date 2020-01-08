FROM mysql:5.7

LABEL maintainer="Pedro Pinheiro <pinheiro.pedrohl@gmail.com>"

ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN chown -R mysql:root /var/lib/mysql/

ADD my.cnf /etc/mysql/conf.d/my.cnf
ADD ./docker-entrypoint-initdb.d/create-testing-databases.sql /docker-entrypoint-initdb.d

CMD ["mysqld"]

EXPOSE 3306
