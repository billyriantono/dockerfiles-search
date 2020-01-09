FROM damm/ubuntu:14.04
MAINTAINER Scott Likens <scott@likens.us>
RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:chris-lea/node.js -y
RUN apt-get update
RUN apt-get install nodejs -y
RUN npm install -g influga
ONBUILD ADD influga-config.json /influga-config.json
ENTRYPOINT influga start -c influga-config.json
