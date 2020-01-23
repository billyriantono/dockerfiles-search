FROM library/node:8.5.0-alpine

RUN npm install -g yo generator-hubot@next &&\
  mkdir /hubot &&\
  adduser -S hubot &&\
  chown hubot /hubot
USER hubot
WORKDIR /hubot
EXPOSE 8080

