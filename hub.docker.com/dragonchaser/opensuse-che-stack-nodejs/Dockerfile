FROM dragonchaser/opensuse-che-stack-base

MAINTAINER Christian Richter<crichter@suse.com>

EXPOSE 1337 3000 4200 5000 9000 8003
LABEL che:server:8003:ref=angular che:server:8003:protocol=http che:server:3000:ref=node-3000 che:server:3000:protocol=http che:server:9000:ref=node-9000 che:server:9000:protocol=http

RUN sudo zypper ref && \
    sudo zypper up -y && \
    sudo zypper install -y nodejs8 npm8
RUN sudo npm install --unsafe-perm -g gulp bower grunt grunt-cli yeoman-generator yo generator-angular generator-karma generator-webapp yarn webpack parcel
