FROM redis:3.2-alpine
MAINTAINER Sean Schoolcraft <seanschoolcraft[@]gmail.com:>

RUN apk update && apk upgrade && apk add --update \
        curl \
        bash \
        sed

ADD redis.conf /etc/redis/redis.conf

COPY run-node.sh /run-node.sh

EXPOSE 6379

RUN chmod 777 /run-node.sh

ENTRYPOINT [ "/run-node.sh" ]
