FROM neo4j:3.2.5
RUN apk update && apk add --no-cache -u python py-pip haproxy bash gawk sed grep bc coreutils ca-certificates
RUN pip install supervisor
RUN set -x \
  && apk add --no-cache --virtual .build-deps \
    curl \
    gcc \
    libc-dev \
    linux-headers \
    make \
    openssl-dev \
    pcre-dev \
    zlib-dev \
  && curl -SL "http://www.haproxy.org/download/1.7/src/haproxy-1.7.9.tar.gz" -o haproxy.tar.gz \
  && echo "a2bbbdd45ffe18d99cdcf26aa992f92d haproxy.tar.gz" | md5sum -c \
  && mkdir -p /usr/src \
  && tar -xzf haproxy.tar.gz -C /usr/src \
  && mv "/usr/src/haproxy-1.7.9" /usr/src/haproxy \
  && rm haproxy.tar.gz \
  && make -C /usr/src/haproxy \
    TARGET=linux2628 \
    USE_PCRE=1 PCREDIR= \
    USE_OPENSSL=1 \
    USE_ZLIB=1 \
    all \
    install-bin \
  && mkdir -p /usr/local/etc/haproxy \
  && cp -R /usr/src/haproxy/examples/errorfiles /usr/local/etc/haproxy/errors \
  && rm -rf /usr/src/haproxy \
  && runDeps="$( \
    scanelf --needed --nobanner --format '%n#p' --recursive /usr/local \
      | tr ',' '\n' \
      | sort -u \
      | awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
  )" \
  && apk add --virtual .haproxy-rundeps $runDeps \
  && apk del .build-deps
COPY conf/haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg
COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY conf/neo4jScript.sh /neo4jScript.sh
RUN chmod +x /neo4jScript.sh
COPY conf/haproxy.sh /haproxy.sh
RUN chmod +x /haproxy.sh
EXPOSE 80
ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisor/conf.d/supervisord.conf"]
