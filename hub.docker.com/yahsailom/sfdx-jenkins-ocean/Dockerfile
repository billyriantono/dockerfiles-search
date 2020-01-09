FROM jenkinsci/blueocean:latest
USER root
RUN apk update && apk upgrade && apk add curl 
RUN apk add nodejs
RUN apk add npm
RUN npm install
RUN npm install sfdx-cli --global
RUN sfdx update
RUN sfdx --version
RUN sfdx plugins --core

USER jenkins
