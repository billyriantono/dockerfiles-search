FROM alpine:latest
LABEL maintainer="Alexey Dubrov <vhsw@ya.ru>" \
      cloned_from="rdsubhas/docker-tor-privoxy-alpine"

RUN apk --no-cache add privoxy tor runit tini

EXPOSE 8118 9050

COPY service /etc/service/

ENTRYPOINT ["tini", "--"]
CMD ["runsvdir", "/etc/service"]
