FROM buildpack-deps:jessie-curl

ENV FILEBEAT_VERSION 1.0.0
ENV FILEBEAT_SHA1 3af2ea90bc3bc9880181503899f82f6a5e852ca8

RUN set -x \
    && curl  -fSL https://download.elastic.co/beats/filebeat/filebeat_${FILEBEAT_VERSION}_amd64.deb -o filebeat.deb \
    && echo "${FILEBEAT_SHA1}  filebeat.deb" | sha1sum -c - \
    && dpkg -i filebeat.deb \
    && rm filebeat.deb

VOLUME ["/etc/filebeat"]

ENTRYPOINT ["filebeat", "-e"]
