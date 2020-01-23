FROM alpine:3.8 as downloader

ENV  DIGDAG_VERSION 0.9.31
RUN  apk add --update --no-cache curl                                                  \
         && curl -o /usr/bin/digdag                                                    \
                 -L "https://dl.digdag.io/digdag-${DIGDAG_VERSION}" \
         && apk -v --purge del curl

FROM java:8-jdk-alpine
COPY --from=downloader /usr/bin/digdag /usr/bin/digdag

ENTRYPOINT ["java", "-jar", "/usr/bin/digdag"]
