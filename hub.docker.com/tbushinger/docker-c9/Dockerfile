FROM ubuntu:16.04

#needed utils
RUN apt-get update && \
    apt-get -y install \
    build-essential \
    curl \
    git \
    g++ \
    libfontconfig \
    python \
    wget

#clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#install node
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
    apt-get install -y nodejs

#setup Met specific git settings
RUN git config --global http.sslVerify false && \
    git config --global url.https://.insteadOf git:// && \
    git config --global user.name abushinger && \
    git config --global user.email abushinger@gmail.com && \
    npm config set registry http://registry.npmjs.org/

VOLUME /root/.c9
VOLUME /root/.npm
VOLUME /root/.node-gyp
VOLUME /root/.cache/bower
VOLUME /workspace

EXPOSE 8080

RUN git clone git://github.com/c9/core.git c9sdk && \
    cd c9sdk && \
    ./scripts/install-sdk.sh

#Metlife setting needed to allow node-gyp to run without errors
ENV NODE_TLS_REJECT_UNAUTHORIZED 0

RUN git config --global user.email abushinger@metlife.com

CMD ["node", "c9sdk/server.js", "-p", "8080", "-l", "0.0.0.0", "-a", "remix:remix", "-w", "/workspace"]
