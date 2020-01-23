FROM resin/raspberrypi3-alpine:edge

LABEL AUTHOR=AnRightHand

ENV ARCH=arm-rbpi
ENV ARIA2_VERSION=1.35.0
ENV ARIA2_URL=https://github.com/q3aql/aria2-static-builds/releases/download/v${ARIA2_VERSION}/aria2-${ARIA2_VERSION}-linux-gnu-${ARCH}-build1.tar.bz2

WORKDIR /app

RUN apk --update --no-cache add bash curl tar && \
  curl -sSL $ARIA2_URL | tar -xj -C /app && \
  mv /app/aria2-${ARIA2_VERSION}-linux-gnu-${ARCH}-build1/aria2c /app/aria2c && \
  mv /app/aria2-${ARIA2_VERSION}-linux-gnu-${ARCH}-build1/ca-certificates.crt /app/ca-certificates.crt && \
  rm -rf /app/aria2-${ARIA2_VERSION}-linux-gnu-${ARCH}-build1 && \
  touch /app/session.lock && \
  chmod +x /app/aria2c
  
VOLUME /config
EXPOSE 6800 6881-6999/udp

CMD /app/aria2c --conf-path=/config/aria2.conf

#RUN curl -sSL -o /app/aria2.conf https://raw.githubusercontent.com/AnRightHand/rpi-dockers/master/aria2/aria2.conf && \
#  curl -sSL -o /app/run.sh https://raw.githubusercontent.com/AnRightHand/rpi-dockers/master/aria2/run.sh && chmod +x /app/run.sh

#CMD /app/run.sh
