FROM ubuntu:16.04

RUN apt-get update && apt-get install wget -y

RUN wget https://repo.percona.com/apt/percona-release_0.1-4.xenial_all.deb
RUN dpkg -i percona-release_0.1-4.xenial_all.deb
RUN apt-get update && apt-get dist-upgrade -y && apt-get install percona-server-mongodb-32 -y

RUN mkdir -p /data/db
RUN mkdir -p /backups

VOLUME ["/data/db"]
VOLUME ["/backups"]

ADD mongod.conf /etc/mongod.conf
ADD /scripts/create-admin.js /create-admin.js
ADD startup.sh /startup.sh
RUN chmod +x /startup.sh

EXPOSE 27017 28017

CMD ["/startup.sh"]
