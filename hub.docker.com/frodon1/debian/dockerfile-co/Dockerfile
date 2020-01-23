FROM alpine:3.2
MAINTAINER Arthur Axel fREW Schmidt <w-pl@afoolishmanifesto.com>

ADD bin/w.sh /bin/w.sh
VOLUME /tmp

RUN apk add --update curl \
 && rm -rf /var/cache/apk/*

ENTRYPOINT ["w.sh"]
CMD ["KBIX", "KSMO"]
