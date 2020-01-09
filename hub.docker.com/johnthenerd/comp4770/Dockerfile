FROM node:10

WORKDIR /turtletale

ADD ./package.json /turtletale/package.json

RUN npm install

RUN mkdir -p /turtletale

ADD . /turtletale

EXPOSE 8080

CMD "npm" "run" "docker"
