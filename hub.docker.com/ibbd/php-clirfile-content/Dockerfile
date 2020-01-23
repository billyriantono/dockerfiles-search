FROM alpine

RUN apk add --no-cache tzdata logrotate

RUN apk --no-cache add curl

ENV TZ Australia/Sydney

COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
