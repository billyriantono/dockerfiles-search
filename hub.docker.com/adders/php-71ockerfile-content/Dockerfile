FROM adaptris/interlok:snapshot-alpine

EXPOSE 8080

WORKDIR /opt/interlok
ADD ant /opt/interlok/ant
ADD config /opt/interlok/config
ADD docker-entrypoint-memorydb.sh /
RUN \
    apk add --no-cache --update apache-ant && \
    rm -f /opt/interlok/adp-*.jar && \
    cd ant && \
    ant -emacs deploy && \
    rm -rf /root/.ivy2/cache/com.adaptris.ui && \
    chmod +x /docker-entrypoint-memorydb.sh && \
    rm -rf /opt/interlok/ant


ENTRYPOINT ["/docker-entrypoint-memorydb.sh"]
