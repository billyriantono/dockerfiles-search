FROM openjdk:8-alpine

EXPOSE 8083

RUN mkdir /commafeed && mkdir /config && mkdir /data
WORKDIR /commafeed

RUN echo Installing packages && \
    apk add \
      --no-cache \
      bash \
      wget

RUN COMMAFEED_VERSION=2.4.0 && \
    \
    DOWNLOAD_URL=https://github.com/Athou/commafeed/releases/download/$COMMAFEED_VERSION/commafeed.jar && \
    echo Downloading $DOWNLOAD_URL to $(pwd) && \
    wget "$DOWNLOAD_URL" --progress bar:force:noscroll --output-document commafeed.jar

WORKDIR /config

RUN COMMAFEED_VERSION=2.4.0 && \
    \
    DOWNLOAD_CONFIG_URL=https://raw.githubusercontent.com/Athou/commafeed/$COMMAFEED_VERSION/config.dev.yml && \
    echo Downloading $DOWNLOAD_CONFIG_URL to $(pwd) && \
    wget "$DOWNLOAD_CONFIG_URL" --progress bar:force:noscroll --output-document config.yml

#VOLUME /config

ENTRYPOINT java -jar /commafeed/commafeed.jar server /config/config.yml
#ENTRYPOINT /bin/bash
