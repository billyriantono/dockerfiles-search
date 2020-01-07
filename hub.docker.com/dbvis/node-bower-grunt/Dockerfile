FROM node:alpine
LABEL MAINTAINER="Wolfgang Jentner <wolfgang.jentner@uni.kn>"


#deps for the rest
RUN apk --update --no-cache add \
        ruby \
        ruby-dev \
        ca-certificates \
        libffi \
        libffi-dev \
        build-base \
        git \
        python \
        curl \
        bash \
    #phantom
    && curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C / \
    #compass stuff
    && gem update --system --no-document \
    && gem install ffi --no-document \
    && gem install compass --no-document \
    #bower & grunt-cli
    && npm i -g bower \
    && npm i -g grunt-cli \
    #cleanup
    && apk del python build-base \
    && rm -rf /usr/share/man /tmp/* /var/tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp
