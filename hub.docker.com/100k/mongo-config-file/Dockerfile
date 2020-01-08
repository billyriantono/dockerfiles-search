FROM mongo:3.2

MAINTAINER Nicolas Zozol - nz@robusta.io - http://www.robusta.io - hk project
# docker pull 100k/mongo-config-file

# Objectif is to use this container with a config file
#  >> sudo docker exec mongo-primary mongo /opt/setup/create-users.js;



# Warning : js script will use this directory
RUN mkdir --parents /opt/conf/ \
    && mkdir --parents /opt/setup/ \
    && mkdir --parents /data/db/ \
    && chown -R mongodb:mongodb /data/db


VOLUME /opt/setup /opt/conf

WORKDIR /opt/conf/

COPY keyfile /opt/conf
COPY mongod.conf /opt/conf

# those arguments will be added to the entrypoint
CMD ["mongod", "-f", "/opt/conf/mongod.conf"]