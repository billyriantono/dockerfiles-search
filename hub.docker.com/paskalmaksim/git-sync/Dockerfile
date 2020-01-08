FROM alpine:latest

ADD . /git-sync

WORKDIR /git-sync

RUN apk --update add yarn npm git nodejs openssh-client \
    && yarn install

CMD yarn repo-init && yarn start

EXPOSE 7954