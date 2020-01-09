FROM alpine:edge

ENV LANG='en_US.UTF-8' \
    LANGUAGE='en_US.UTF-8' \
    TERM='xterm'

RUN echo http://dl-4.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories && \
  apk -U upgrade && \
  apk -U add \
    ca-certificates \
    emby \
    && \
  apk del make gcc g++ && \
  rm -rf /tmp/src && \
  rm -rf /var/cache/apk/*


ADD start.sh /
RUN chmod +x /start.sh

#http port
EXPOSE 8096
#https port
EXPOSE 8920
EXPOSE 7359/udp
EXPOSE 1900/udp

CMD ["/start.sh"]
