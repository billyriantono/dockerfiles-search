FROM ismeade/maven:3.5.0

MAINTAINER ismeade <ismeade99@sina.com>

RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

VOLUME /git
WORKDIR /git

CMD ["git", "--version"]
