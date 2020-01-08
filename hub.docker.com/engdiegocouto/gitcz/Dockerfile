FROM node:alpine

LABEL MAINTAINER="Diego do Couto <https://github.com/engdiegocouto>"

ENV GITCZ_APP_DIR=/opt/gitcz \
    GITCZ_USER_NAME=gitcz \
    GITCZ_USER_UID=10001

ENV GIT_CONFIG_NAME="Git User"\
    GIT_CONFIG_EMAIL="gitcz@gitcz.local"

ENV PATH=${GITCZ_APP_DIR}:${PATH}\
    HOME=${GITCZ_APP_DIR}

WORKDIR /gitcz/data

COPY uid_entrypoint /usr/bin

RUN apk --update add git && \
    npm install -g commitizen && \
    npm install -g cz-conventional-changelog && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/* 

RUN adduser -u ${GITCZ_USER_UID} -S -D -h ${GITCZ_APP_DIR} -g "${GITCZ_USER_NAME} user" -s /sbin/nologin ${GITCZ_USER_NAME} && \
    mkdir -p /gitcz/data && \
    chmod a+x /usr/bin/uid_entrypoint && \
    chown -R ${GITCZ_USER_UID}:root /gitcz/data /opt/gitcz && \
    chmod -R g=u /gitcz/data /etc/passwd

USER ${GITCZ_USER_UID}

VOLUME [ "/gitcz/data", "/opt/gitcz/" ]

ENTRYPOINT [ "uid_entrypoint" ]