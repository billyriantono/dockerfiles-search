FROM alpine:3.8 as downloader

ENV  EMBULK_VERSION 0.9.9
RUN  apk add --update --no-cache curl                                                  \
         && curl -o /usr/bin/embulk                                                    \
                 -L "https://dl.bintray.com/embulk/maven/embulk-${EMBULK_VERSION}.jar" \
         && apk -v --purge del curl

FROM java:8-jdk-alpine
COPY --from=downloader /usr/bin/embulk /usr/bin/embulk
RUN  chmod 755 /usr/bin/embulk \
         && apk -v --update add python            \
                                py-pip            \
                                groff             \
                                less              \
                                mailcap           \
         && pip install --upgrade awscli==1.16.52 \
         && apk -v --purge del py-pip             \
         && rm /var/cache/apk/*

VOLUME /root/.aws

