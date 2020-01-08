FROM node:argon
MAINTAINER Jens Peter Secher <jp@openmono.com>
RUN mkdir -p /usr/src/grapher
WORKDIR /usr/src/grapher
COPY package.json setup-production-env.sh /usr/src/grapher/
RUN ./setup-production-env.sh
COPY . /usr/src/grapher
RUN ./setup-node-env.sh
EXPOSE 3000
CMD [ "npm", "start" ]
