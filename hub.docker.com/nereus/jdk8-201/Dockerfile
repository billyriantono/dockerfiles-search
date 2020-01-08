FROM kwonghung/docker-jdk:8.0.201-oracle
LABEL maintainer="kwonghung.yip@gmail.com"

RUN apt-get update && apt-get -y install gnupg \
  && curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list \
  && apt-get update \
  && apt-get -y install google-chrome-stable

ENV DBUS_SESSION_BUS_ADDRESS=/dev/null

ENV TINI_VERSION v0.18.0

ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini

RUN chmod +x /tini

ENTRYPOINT ["/tini", "--"]