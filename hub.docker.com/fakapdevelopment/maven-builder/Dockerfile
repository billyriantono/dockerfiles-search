FROM maven:alpine

RUN apk add --no-cache \
    git openssh gawk \
    python python-dev py-pip \
    && pip install awscli \
    && pip install --upgrade pip

ENV GIT_USER_NAME=''
ENV GIT_USER_EMAIL=''

COPY .m2 /root/.m2
COPY build-hooks /usr/local/bin
COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
