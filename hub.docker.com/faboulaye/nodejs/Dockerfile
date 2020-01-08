FROM debian:8
MAINTAINER Firdaws Aboulaye "aboufred@gmail.com"

ENV WEBAPP=/webapp

LABEL webapp.dir="$WEBAPP"

RUN apt-get update -y \
  && apt-get --no-install-recommends -y install curl sudo git \
  && curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
  && apt-get install --no-install-recommends --fix-missing -y nodejs npm build-essential \
  && ln -s /usr/bin/nodejs /usr/bin/node \
  && mkdir webapp \
  && apt-get remove -y curl \
  && apt-get clean \
  && rm -rf /tmp/* /var/log/* /var/cache/* /usr/share/man/?? /usr/share/man/??_* /var/lib/apt/lists/* \
  && nodejs -v

VOLUME ["$WEBAPP"]
WORKDIR $WEBAPP
EXPOSE 7000-9000

CMD ["bash"]
