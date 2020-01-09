ARG IMG_VERSION=0.5.7

FROM r.j3ss.co/img:v${IMG_VERSION} AS img-upstream

FROM buildkite/agent:3

COPY --from=img-upstream /usr/bin/img /usr/bin/img
COPY --from=img-upstream /usr/bin/newuidmap /usr/bin/newuidmap
COPY --from=img-upstream /usr/bin/newgidmap /usr/bin/newgidmap

RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing gosu && \
    chmod u+s /usr/bin/newuidmap /usr/bin/newgidmap && \
    adduser -D -u 1000 user && \
    mkdir -p /run/user/1000 && \
    chown -R user /run/user/1000 /home/user && \
    echo user:100000:65536 | tee /etc/subuid | tee /etc/subgid

COPY scripts/bk-img /usr/bin/bk-img