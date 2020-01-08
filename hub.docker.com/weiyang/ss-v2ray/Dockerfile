FROM alpine as builder
ARG WORKSPACE=/ss-v2ray
ARG RELEASE_URL=https://github.com/shadowsocks/v2ray-plugin/releases/download/v1.1.0/v2ray-plugin-linux-amd64-v1.1.0.tar.gz

RUN set -ex \
    && apk add --no-cache wget \
                          tar \
    && mkdir -p ${WORKSPACE} \
    && cd ${WORKSPACE} \
    && wget ${RELEASE_URL} \
    && tar zxf $(basename ${RELEASE_URL})

FROM alpine
ENV REPO shadowsocks/v2ray-plugin
ARG BIN=/ss-v2ray/v2ray-plugin_linux_amd64
COPY --from=builder ${BIN}/ /usr/bin/v2ray-plugin

CMD ["v2ray-plugin"]
