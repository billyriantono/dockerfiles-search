FROM alpine:latest

MAINTAINER wizjin <wizjin@users.noreply.github.com>

RUN apk add --update --no-cache privoxy

ADD privoxy-start.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/privoxy-start.sh

CMD ["privoxy-start.sh"]

EXPOSE 8118

