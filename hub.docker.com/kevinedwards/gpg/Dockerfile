FROM alpine:latest

MAINTAINER Kevin Edwards <kewards@kevinedwards.ca>

ENV BUILD_DEPS ""

ENV PACKAGES "openrc openssh gnupg"

RUN apk add --no-cache --virtual=build-dependencies ${BUILD_DEPS} && \
    apk add --no-cache ${PACKAGES} && \
    rc-update add sshd && \
    apk del build-dependencies

VOLUME /project

WORKDIR /project

CMD ["gpg", "-h"]
ENTRYPOINT ["gpg"]
