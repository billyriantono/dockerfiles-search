ARG DEBIAN_VERSION

FROM debian:$DEBIAN_VERSION as dl

ARG ALIYUNCLI_VERSION

ADD https://github.com/aliyun/aliyun-cli/releases/download/v${ALIYUNCLI_VERSION}/aliyun-cli-linux-${ALIYUNCLI_VERSION}-amd64.tgz /tmp/aliyun-cli-linux-amd64.tgz

RUN tar zxvf /tmp/aliyun-cli-linux-amd64.tgz -C /tmp


FROM debian:$DEBIAN_VERSION

COPY --from=dl /tmp/aliyun /usr/local/bin/aliyun

CMD ["aliyun"]
