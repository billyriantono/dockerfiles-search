# ---- Docker based ----
FROM docker:stable

#Set the timezone to Paris
ENV TZ=Europe/Paris

RUN \
    apk update \
    # install bash git jq util-linux nodejs npm
    && apk add --update --no-cache bash jq util-linux nodejs npm \
    && which ssh-agent || ( apk add openssh-client ) \
    # cleanup
    && rm /var/cache/apk/* \
    && rm -rf /var/lib/apk/
