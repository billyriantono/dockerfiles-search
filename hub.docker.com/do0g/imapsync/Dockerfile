FROM alpine

MAINTAINER Doug Hardy "do0g.dev@gmail.com"

RUN echo @testing http://nl.alpinelinux.org/alpine/edge/testing >> etc/apk/repositories \
 && apk --no-cache add imapsync@testing

ENTRYPOINT ["imapsync"]
