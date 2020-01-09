FROM node
MAINTAINER Scott Coulton "https://github.com/scotty-c/docker-norrisbot"

CMD ["/bin/bash", "-l"]

RUN apt-get -qqy update
RUN npm install -g norrisbot

ENV NORRISBOT_TOKEN=""

ENTRYPOINT 'norrisbot'


