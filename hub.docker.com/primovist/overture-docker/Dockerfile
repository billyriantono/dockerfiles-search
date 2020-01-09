FROM alpine
ARG OT_VER=1.5
ARG OT_URL=https://github.com/shawn1m/overture/releases/download/v$OT_VER/overture-linux-amd64.zip
LABEL maintainer="primovist" \
        org.label-schema.name="overture-docker" \
        org.label-schema.version=$OT_VER
RUN cd /root && \
    wget --no-check-certificate -O overture.zip $OT_URL && \
    unzip overture.zip && \
    chmod +x overture-linux-amd64 && \
    mv overture-linux-amd64 /usr/bin/overture && \
    rm -rf ./*
CMD overture -c /etc/overture/config.json
