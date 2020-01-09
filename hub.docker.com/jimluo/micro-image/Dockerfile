FROM alpine:3.6

ENV FILEBEAT_VERSION 5.5.0
RUN sed -i "s|http://dl-cdn.alpinelinux.org|https://mirrors.ustc.edu.cn|g" /etc/apk/repositories
RUN set -x; \
    apk add --no-cache bash vim curl tar openssl openssl-dev ca-certificates \
    && curl -O -L https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz \
    && tar -C /usr/local -xvf filebeat-${FILEBEAT_VERSION}-linux-x86_64.tar.gz 
RUN ln -sf  /usr/local/filebeat-${FILEBEAT_VERSION}-linux-x86_64/filebeat /bin/filebeat
WORKDIR /etc/filebeat/
# COPY ./filebeat-conf /etc/filebeat
