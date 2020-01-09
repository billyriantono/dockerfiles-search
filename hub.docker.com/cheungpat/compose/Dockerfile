FROM alpine:3.7

RUN apk add --update --no-cache python3 docker \
    && pip3 install docker-compose==1.20.1
ENTRYPOINT ["docker-compose"]
