FROM ubuntu:14.04
MAINTAINER Conjur Inc

RUN apt-get update && apt-get install -y build-essential g++ flex bison gperf ruby ruby-dev perl libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev libpng-dev libjpeg-dev python git npm && ln -s /usr/bin/nodejs /usr/bin/node

ADD phantomjs /opt/phantomjs
WORKDIR /opt/phantomjs
RUN ./build.sh --confirm && ln -s /opt/phantomjs/bin/phantomjs /usr/local/bin/phantomjs
