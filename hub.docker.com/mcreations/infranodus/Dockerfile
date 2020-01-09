## -*- docker-image-name: "mcreations/infranodus" -*-

FROM node:8

MAINTAINER Kambiz Darabi <darabi@m-creations.net>

ENV INFRA_HOME /opt/infranodus
ENV NEO4J_USER neo4j
ENV NEO4J_PASSWORD password

ENV CORS "http://localhost:3000"

ADD . $INFRA_HOME/

RUN npm install forever -g &&\
    cd $INFRA_HOME &&\
    cp config.json.sample config.json &&\
    npm install npm@latest -g &&\
    npm install -g forever &&\
    npm install

EXPOSE 3001
CMD [ "/opt/infranodus/bin/start-infranodus" ]

# CMD ["/usr/bin/forever","$INFRA_HOME/app.js"]
