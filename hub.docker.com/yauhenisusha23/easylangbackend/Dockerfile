FROM ubuntu:18.04

RUN apt-get update && apt-get install -y curl sudo && \
    apt-get install -y --no-install-recommends apt-utils && \
    apt-get install -y postgresql && /etc/init.d/postgresql start && \
    sudo su - postgres -c "psql -c \"CREATE USER admin WITH PASSWORD 'admin' CREATEDB;\"" && \
    sudo su - postgres -c "psql -c \"CREATE DATABASE easy OWNER admin;\""
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash
RUN apt-get install -y nodejs build-essential

WORKDIR /var/www/API
COPY . /var/www/API/

RUN yes | npm i pm2 -g && npm i

EXPOSE 3000
CMD sudo /etc/init.d/postgresql restart && pm2 start app.js && pm2 logs