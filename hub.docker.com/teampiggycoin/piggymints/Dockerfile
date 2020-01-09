#BUILDS: teampiggycoin/piggymints

FROM teampiggycoin/piggycoind
MAINTAINER Team PiggyCoin <team@piggy-coin.com>

ENV APP_DIR /piggymints
ENV APP_REPO https://github.com/TeamPiggyCoin/PiggyMints-WebUI.git

# Install python3 & piggymints (a fork of TheSeven/Bitcoin-WebUI)
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
 && apk-install --update python3 python3-dev build-base git openssl \
 && pip3 install --upgrade --no-cache-dir pip setuptools \
 && git clone $APP_REPO $APP_DIR \
 && apk del build-base git

# Install piggymints service
ADD . /
RUN chmod a+x /etc/service/piggymints/run

EXPOSE 8338 54481
VOLUME /root/.newpiggycoin
WORKDIR /root/.newpiggycoin
ENTRYPOINT ["/sbin/runit-docker"]
