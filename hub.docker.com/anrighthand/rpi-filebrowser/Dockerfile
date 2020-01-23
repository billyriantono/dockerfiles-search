FROM resin/raspberrypi3-alpine:edge

LABEL AUTHOR=AnRightHand

ENV ARCH=armv7
ENV FILE_BROWSER_VERSION=v2.0.16
ENV FILE_BROWSER_URL=https://github.com/filebrowser/filebrowser/releases/download/${FILE_BROWSER_VERSION}/linux-${ARCH}-filebrowser.tar.gz

WORKDIR /app

RUN apk --update --no-cache add bash curl tar && \
  curl -sSL $FILE_BROWSER_URL | tar -zx -C /app && \
  chmod +x /app/filebrowser

EXPOSE 80 443

CMD /app/filebrowser --config /.filebrowser.json

#RUN curl -sSL -o /app/filebrowser.json https://raw.githubusercontent.com/AnRightHand/rpi-dockers/master/filebrowser/filebrowser.json && \
#  curl -sSL -o /app/run.sh https://raw.githubusercontent.com/AnRightHand/rpi-dockers/master/filebrowser/run.sh && chmod +x /app/run.sh

#CMD /app/run.sh
