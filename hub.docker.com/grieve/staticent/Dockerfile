FROM alpine:3.11

RUN apk add --update --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing runc buildah 
COPY registries.conf /etc/containers/registries.conf
ADD https://raw.githubusercontent.com/containers/skopeo/master/default-policy.json /etc/containers/policy.json
ENV STORAGE_DRIVER "vfs"