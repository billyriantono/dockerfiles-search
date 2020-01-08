FROM alpine:3.9.2

COPY . /aliyuncli
VOLUME [ /aliyuncli ]

RUN \
  apk add --no-cache curl jq && \
  curl -o aliyun.tgz "https://aliyuncli.alicdn.com/aliyun-cli-linux-3.0.2-amd64.tgz?spm=a2c4g.11186623.2.13.6cc417a46c7MqY&file=aliyun-cli-linux-3.0.2-amd64.tgz" && \
  tar -xzvf aliyun.tgz &&  mv aliyun /usr/local/bin/ && \
  rm -rf /tmp/*

WORKDIR /aliyuncli

# ENTRYPOINT [ "/aliyuncli/entrypoint.sh" ]