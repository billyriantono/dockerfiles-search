FROM node:6.9.5-slim

RUN apt-get update && apt-get install -y libldap2-dev

# Create app directory
RUN mkdir -p /usr/src/app/log && \
    mkdir /usr/src/app/service-account && \
    mkdir /usr/src/app/src

WORKDIR /usr/src/app

ADD package.json /usr/src/app/
RUN npm install

ADD src /usr/src/app/src
ADD docker-entrypoint.sh /usr/src/app/ 

RUN npm run build

VOLUME ["/service-account"]

EXPOSE 8080
ENTRYPOINT ["/usr/src/app/docker-entrypoint.sh"]