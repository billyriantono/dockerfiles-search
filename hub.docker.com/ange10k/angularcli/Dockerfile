############################################################
# Dockerfile
############################################################

# Set the base image
FROM node:10-alpine

############################################################
# Configuration
############################################################
ENV VERSION "8.3.4"

############################################################
# Installation
############################################################
RUN apk --no-cache add bash &&\
    apk --no-cache add curl &&\
    apk --no-cache add lftp ca-certificates openssh bash curl
    
RUN npm install -g @angular/cli@${VERSION}

RUN mkdir -p /workdir
VOLUME /workdir
WORKDIR /workdir

############################################################
# Execution
############################################################
ENTRYPOINT []
CMD [ "ng", "--help"]
