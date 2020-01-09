FROM ubuntu:bionic AS build
WORKDIR /build
COPY ffmpeg.sh /build/.
RUN ./ffmpeg.sh

FROM ubuntu:bionic
RUN apt-get -y update && \
    apt-get install -y --no-install-recommends curl ca-certificates && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    apt-get -y update && \
    apt-get install -y --no-install-recommends nodejs libavahi-compat-libdnssd-dev && \
    rm -rf /var/lib/apt/lists/* && \
    npm install -g homebridge && \
    npm install -g homebridge-camera-ffmpeg
COPY --from=build /build/bin/ffmpeg /usr/bin/.
CMD homebridge
