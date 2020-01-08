FROM kuwas/alpine:bash
MAINTAINER kuwas/dockerfiles

# install #

RUN apk add --update \
      curl \
      git \
      openssh \
      openssl \
      tar \
      wget \
      ;
RUN rm -rf /var/cache/apk/*

# cmd #

CMD [ "bash" ]
