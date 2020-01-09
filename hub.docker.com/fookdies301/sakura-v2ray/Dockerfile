FROM alpine:3.9.4@sha256:769fddc7cc2f0a1c35abb2f91432e8beecf83916c421420e6a6da9f8975464b6 as V2ray

RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.9/main/" >> /etc/apk/repositories \
  && apk upgrade --no-cache \
  && apk --update --no-cache add ca-certificates curl wget unzip grep \
  && rm -rf /var/cache/apk/*

RUN mkdir /usr/bin/v2ray \
  && cd /usr/bin/v2ray \
  && VER=$(curl -s https://api.github.com/repos/v2ray/v2ray-core/releases/latest | grep tag_name | awk  -F '"' '{print $4}') \
  && wget https://github.com/v2ray/v2ray-core/releases/download/$VER/v2ray-linux-64.zip \
  && unzip v2ray-linux-64.zip \
  && rm -rf v2ray-linux-64.zip \
  && chmod +x /usr/bin/v2ray/*
COPY ./v2ray /v2ray

FROM alpine:3.9.4@sha256:769fddc7cc2f0a1c35abb2f91432e8beecf83916c421420e6a6da9f8975464b6

COPY --from=V2ray /usr/bin/v2ray /usr/bin/v2ray
ENV PATH=$PATH:/usr/bin/v2ray

COPY --from=V2ray /v2ray /v2ray
RUN chmod +x /v2ray/docker-entrypoint.sh

ENV DOCKER_ENV=true
ENTRYPOINT [ "/v2ray/docker-entrypoint.sh" ]

WORKDIR /v2ray

CMD [ "v2ray", "-config", "/v2ray/config.jsonc" ]
