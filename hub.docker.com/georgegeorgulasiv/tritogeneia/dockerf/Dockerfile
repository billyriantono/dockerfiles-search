# Build The Latest Version Of Ansible
FROM alpine:3

ENV IMAGE_USER="user" \
    IMAGE_UID="1000" \
    IMAGE_GID="1000"

# Create A Default User To Replace Root User
# hadolint ignore=DL3018,DL3019
RUN apk update && apk add ansible && \
    addgroup -g ${IMAGE_GID} ${IMAGE_USER} && \
    adduser -D -u ${IMAGE_UID} -G ${IMAGE_USER} ${IMAGE_USER} && \
    mkdir /project && \
    chown "${IMAGE_USER}":"${IMAGE_USER}" /project

# Container Settings
WORKDIR /project
USER ${IMAGE_USER}
CMD ["/bin/sh"]
