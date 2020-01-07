FROM gabrielrezzonico/docker-node:0.0.1

MAINTAINER Gabriel Rezzonico <gabrielrezzonico@gmail.com>

#Node, Ionic ENVs
# version to be installed
ENV BOWER_VERSION=1.7.9 \
    CORDOVA_VERSION=6.1.1 \
    GRUNT_VERSION=1.0.1 \
    GULP_VERSION=3.9.1 \
    IONIC_VERSION=1.7.14

# change to user 
USER ${DOCKER_USER}
WORKDIR /home/${DOCKER_USER}/

#install nvm first, then node using nvm, and the rest of the apckages using npm
RUN export NVM_DIR="/home/docker-user/.nvm" \
    && [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" \
    && npm install -g grunt-cli@${GRUNT_VERSION} \
    bower@${BOWER_VERSION} \
    cordova@${CORDOVA_VERSION} \
    grunt-cli@${GRUNT_VERSION} \
    gulp@${GULP_VERSION} \
    ionic@${IONIC_VERSION}

ENTRYPOINT ["/bin/bash","-l"]


