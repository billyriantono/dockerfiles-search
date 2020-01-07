FROM mongo:3.7.3-jessie

RUN mkdir /opt/insync-db

ADD . /opt/insync-db

RUN chmod +x ./opt/insync-db/start.sh &&\
  touch /var/log/mongod.log

RUN mkdir /data/insync

ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 27017

RUN mongod --fork --logpath /var/log/mongod.log --dbpath=/data/insync

CMD opt/insync-db/start.sh &&\
  tail -f /var/log/mongod.log
