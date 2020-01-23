FROM resin/raspberrypi3-alpine:edge

LABEL AUTHOR=AnRightHand

ENV ARCH=arm
ENV SYNCTHING_VERSION=1.3.2
ENV SYNCTHING_URL=https://github.com/syncthing/syncthing/releases/download/v${SYNCTHING_VERSION}/syncthing-linux-${ARCH}-v${SYNCTHING_VERSION}.tar.gz

EXPOSE 8384 22000 21027/UDP
VOLUME /config /sync

RUN addgroup \
    -S -g 1000 \
    syncthing && \
  adduser \
    -S -H -D \
    -s /bin/bash \
    -u 1000 \
    -G syncthing \
    syncthing 
  
WORKDIR /app

RUN apk --update --no-cache add bash curl tar && \
  curl -sSL $SYNCTHING_URL | tar -zx -C /app && \
  mv /app/syncthing-linux-${ARCH}-v$SYNCTHING_VERSION/* /app && \
  rm -rf /app/syncthing-linux-${ARCH}-v$SYNCTHING_VERSION && \
  chmod +x /app/syncthing && \
  chmod -R 777 /app && \
  chmod -R 777 /config && \
  chmod -R 777 /sync


USER syncthing

CMD /app/syncthing -home /config/ -no-browser -gui-address 0.0.0.0:8384
