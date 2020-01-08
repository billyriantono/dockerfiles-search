FROM alpine/git

LABEL maintainer Perrin Ennen <hello@perrinennen.de>

RUN apk update && apk upgrade && \
    apk add --no-cache bash wget git openssh openssh-client && \
    apk add jq curl curl-dev