FROM node:12.14-stretch

LABEL "maintainer"="FreeHackQuest Team <freehackquest@gmail.com>"
LABEL "repository"="https://github.com/freehackquest/angular-cli-start"

RUN bash -c 'echo N | npm install -g @angular/cli'

EXPOSE 4200
WORKDIR /home/node
COPY ./start-in-docker.sh /home/node/start-in-docker.sh
CMD ./start-in-docker.sh