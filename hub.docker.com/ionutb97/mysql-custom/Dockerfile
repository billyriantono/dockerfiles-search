FROM mysql:5.7

ENV MYSQL_DATABASE 'download_speed_aws'
ENV MYSQL_USER 'admin'
ENV MYSQL_PASSWORD 'admin1337'
ENV MYSQL_ROOT_PASSWORD 'admin1337'

ADD ./sql/ /docker-entrypoint-initdb.d/
ADD ./config/my.cnf /etc/mysql/conf.d/my.cnf

RUN apt-get update \
 && apt-get install --no-install-recommends -y tzdata \
 && apt-get clean \
 && rm -r /var/lib/apt/lists/*
