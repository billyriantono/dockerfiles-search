FROM alpine:3.11

RUN apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing crun podman conmon cni-plugins

COPY ./libpod.conf /etc/containers/libpod.conf
COPY ./registries.conf /etc/containers/registries.conf
ADD https://raw.githubusercontent.com/containers/skopeo/master/default-policy.json /etc/containers/policy.json
ADD https://raw.githubusercontent.com/containers/libpod/master/cni/87-podman-bridge.conflist /etc/cni/net.d/87-podman-bridge.conf

ENV STORAGE_DRIVER "vfs"