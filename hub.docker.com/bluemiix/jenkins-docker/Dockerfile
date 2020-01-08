FROM jenkins/jenkins:lts-alpine

USER root

RUN rm -rf /var/cache/apk/* \
# install NodeJS
    && apk --update add nodejs \
# Test
    && node -v \
    && npm -v

USER jenkins