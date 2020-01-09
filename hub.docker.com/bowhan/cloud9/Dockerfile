FROM ubuntu:18.04

RUN apt-get update -qq \
    && apt-get install -y -qq \
        build-essential \
        git \
        curl \
        python2.7 \
    && curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y -qq nodejs

RUN apt-get install -y -qq locales && locale-gen en_US.UTF-8

RUN git clone https://github.com/c9/core.git /c9sdk \
    && cd /c9sdk \
    && scripts/install-sdk.sh

EXPOSE 8008

ENV WD=/wd
ENV USERNAME=user
ENV PASSWORD=pwd

CMD node /c9sdk/server.js \
    --listen 0.0.0.0 \
    --port 8008 \
    -w $WD \
    --auth $USERNAME:$PASSWORD