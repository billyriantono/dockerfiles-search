FROM mysql:5.7.15

MAINTAINER abelfadel<abdelhadi.belfadel@gmail.com>

ENV MYSQL_DATABASE=fitman \
    MYSQL_ROOT_PASSWORD=fitman

ADD fitman_3dscan_webgl.sql /docker-entrypoint-initdb.d

EXPOSE 3306