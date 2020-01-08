FROM node:8.15.1-stretch-slim

RUN apt-get update && \
    apt-get install -y git gosu && \
# verify that the binary works
    gosu nobody true && \
# install bower and polymer-cli
	npm install -g bower polymer-cli --unsafe-perm && \
# cleanup
    rm -rf /var/lib/apt/lists/* && rm -rf /tmp/*

WORKDIR /tmp
ENTRYPOINT ["gosu","node"]
