FROM docker.io/node:10-stretch

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y --no-install-recommends chromium=70.0.3538.110-1~deb9u1 \
    && apt-get install -y --no-install-recommends chromium-driver=70.0.3538.110-1~deb9u1 \
    && apt-get install -y --no-install-recommends chromedriver=70.0.3538.110-1~deb9u1

ENV CHROME_BIN=chromium

WORKDIR /usr/src/app
CMD [ "node" ]
