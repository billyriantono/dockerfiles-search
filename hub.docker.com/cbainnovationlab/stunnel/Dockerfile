FROM alpine:3.8
LABEL maintainer="dan.turner@cba.com.au"

RUN apk add --no-cache stunnel \
 && addgroup -g 1000 -S app \
 && adduser -u 1000 -S app -G app

USER app

WORKDIR /etc/stunnel/
VOLUME /etc/stunnel/

CMD ["stunnel"]
