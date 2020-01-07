FROM node:9-alpine
MAINTAINER Patrick Hempel <patrick@hempel.io>

#RUN apt-get update && apt-get install -y build-essential python inotify-tools
RUN npm install -g npm@3.10.8
RUN npm install -g @angular/cli@latest
#RUN apt-get purge -y build-essential
RUN mkdir /data
VOLUME /data
WORKDIR /data
EXPOSE 4200
EXPOSE 49153
CMD ng serve --host 0.0.0.0
