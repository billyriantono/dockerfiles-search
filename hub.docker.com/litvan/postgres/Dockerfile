FROM postgres:9.6.8

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list &&\
    apt-get update && apt-get install wget -y &&\
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
    apt-key add - &&\
    apt-get update &&\
    apt-get install postgresql-9.6-postgis-2.3 -y

CMD ["postgres"]


