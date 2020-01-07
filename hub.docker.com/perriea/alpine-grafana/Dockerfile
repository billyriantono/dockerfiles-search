FROM alpine:3.7

LABEL MAINTAINER="Aurelien PERRIER <a.perrier89@gmail.com>"
LABEL APP="grafana"
LABEL APP_REPOSITORY="https://github.com/grafana/grafana/releases"

ENV TIMEZONE Europe/Paris

ENV GRAFANA_VERSION 5.0.4
ENV GLIBC_VERSION 2.27-r0
ENV GF_INSTALL_PLUGINS ""

# Installing packages
RUN apk add --no-cache su-exec ca-certificates openssl
RUN apk add --no-cache --virtual .build-deps fontconfig

# Work path
WORKDIR /scripts

# Downloading binaries    
ADD https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-${GRAFANA_VERSION}.linux-x64.tar.gz ./
ADD https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub /etc/apk/keys/
ADD https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk ./
RUN addgroup grafana && \
    adduser -s /bin/false -G grafana -S -D grafana

RUN apk add ./glibc-${GLIBC_VERSION}.apk
RUN rm /etc/apk/keys/sgerrand.rsa.pub glibc-${GLIBC_VERSION}.apk

# Coping config & scripts
COPY ./scripts/start.sh start.sh

RUN tar -C . -xzf grafana-$GRAFANA_VERSION.linux-x64.tar.gz && \
        mv grafana-${GRAFANA_VERSION} /grafana && \
        mkdir -p /var/lib/grafana/dashboards /var/lib/grafana/data /var/lib/grafana/logs /var/lib/grafana/plugins && \
        ln -s /grafana/plugins /var/lib/grafana/plugins && \
        mv /grafana/bin/* /usr/bin/ && \
        grafana-cli plugins update-all && \
        rm -f /grafana/conf/*.ini grafana-$GRAFANA_VERSION.linux-x64.tar.gz && \
        apk del .build-deps

COPY ./files/defaults.ini /grafana/conf/

VOLUME  [ "/grafana" ]

EXPOSE 3000

ENTRYPOINT ["sh", "start.sh"]