FROM docker:git

MAINTAINER Sascha Selzer sascha.selzer@gmail.com

RUN apk --no-cache add ca-certificates jq && \
    wget \
        "https://raw.githubusercontent.com/sgerrand/alpine-pkg-git-crypt/master/sgerrand.rsa.pub" \
        -O "/etc/apk/keys/sgerrand.rsa.pub"  && \
    wget "https://github.com/sgerrand/alpine-pkg-git-crypt/releases/download/0.6.0-r0/git-crypt-0.6.0-r0.apk" && \
    apk --no-cache add git-crypt-0.6.0-r0.apk && \
    rm "/etc/apk/keys/sgerrand.rsa.pub" && \
    rm git-crypt-0.6.0-r0.apk && \
    apk del ca-certificates