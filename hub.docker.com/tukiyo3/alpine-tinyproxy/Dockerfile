FROM alpine

RUN set -xe \
  && apk add --no-cache tinyproxy
EXPOSE 8888
COPY conf/tinyproxy.conf /etc/tinyproxy/tinyproxy.conf
CMD ["tinyproxy", "-d"]
VOLUME /etc/tinyproxy/
