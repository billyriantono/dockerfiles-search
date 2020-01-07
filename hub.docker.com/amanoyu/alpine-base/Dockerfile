FROM alpine:latest
MAINTAINER "amanoyu" <alterna_cloud@me.com>

ENV PATH $PATH:/usr/bin

RUN \
  apk update && \
  apk --no-cache add bash vim curl wget which supervisor htop tzdata git && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  apk del tzdata && \
  rm -rf /var/cache/apk/*

  ADD etc /etc
  COPY sh/startup.sh /tmp/

  RUN  chmod a+x /tmp/startup.sh

  EXPOSE 80 443
  ENTRYPOINT ["/tmp/startup.sh"]
