FROM node:4.4.7

RUN apt-get update && \
BUILD_PACKAGES="mercurial git curl wget vim" && \
apt-get -y install $BUILD_PACKAGES

RUN echo '{ "allow_root": true }' > /root/.bowerrc

#WORKDIR /usr/src/app

COPY setup.sh /setup.sh
COPY deploy.sh /deploy.sh
COPY start.sh /start.sh
COPY bin/server /usr/bin/go-server
COPY crt/server.crt /usr/crt/server.crt
COPY crt/server.key /usr/crt/server.key

VOLUME ["/usr/src/app", "/root/.ssh"]

EXPOSE 443

ENTRYPOINT ["/bin/bash", "/start.sh"]