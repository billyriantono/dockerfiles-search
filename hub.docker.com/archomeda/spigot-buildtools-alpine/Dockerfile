FROM openjdk:8-alpine

LABEL maintainer "Archomeda (https://github.com/Archomeda/spigot-buildtools-docker)"

ENV REVISION "latest"

# Install openssl and git
RUN apk add --no-cache openssl git bash

# Add script
COPY build.sh /root/build.sh
RUN chmod +x /root/build.sh

RUN mkdir /build
VOLUME /build
WORKDIR /build

CMD ["bash", "/root/build.sh"]
