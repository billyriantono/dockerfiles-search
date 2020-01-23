FROM alpine:latest

RUN apk upgrade -U && \
    apk --no-cache --update --repository=http://dl-4.alpinelinux.org/alpine/edge/testing add -u \
    git \
    openssh-client \
    yarn \
    && yarn global add commitizen cz-conventional-changelog standard-version \
    && echo '{ "path": "cz-conventional-changelog"  }' > ~/.czrc \
    && rm -fr /var/cache/apk/* \
    && git config --global user.email "drone@gmail.com" \
    && git config --global user.name "Drone"

COPY drone-changelog-tag /usr/local/bin/drone-changelog-tag

