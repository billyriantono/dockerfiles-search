from alpine

maintainer Jonathan Homer

run apk update && apk upgrade && \
    apk add --no-cache bash git openssh

ENV TOKEN none
ENV GIT none

VOLUME /clone

WORKDIR /clone

CMD ["sh","-c","git clone https://${TOKEN}:x-oauth-basic@github.com/${GIT}"]
