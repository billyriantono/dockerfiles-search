FROM alpine:3.10
MAINTAINER Josh.5 "jsunnex@gmail.com"

################
### CONFIG:
###
# set version for s6 overlay
ARG OVERLAY_VERSION="v1.22.1.0"
ARG OVERLAY_ARCH="amd64"
ENV PS1="$(whoami)@$(hostname):$(pwd)$ "


RUN \
    echo "**** install base packages ****" && \
        apk add --no-cache \
            bash \
            ca-certificates \
            coreutils \
            curl \
            nano \
            shadow \
            tar \
            unzip \
            tzdata \
        && \
    echo "**** add s6 overlay ****" && \
        curl -o \
            /tmp/s6-overlay.tar.gz -L \
            "https://github.com/just-containers/s6-overlay/releases/download/${OVERLAY_VERSION}/s6-overlay-${OVERLAY_ARCH}.tar.gz" && \
        tar xfz \
            /tmp/s6-overlay.tar.gz -C / \
        && \
    echo "**** create docker user and make our folders ****" && \
        groupmod -g 1000 users && \
        useradd -u 1000 -U -d /config -s /bin/false docker && \
        usermod -G users docker && \
        mkdir -p \
            /app \
            /config \
            /defaults \
        && \
    echo "**** cleanup ****" && \
        rm -rf /tmp/*


# add local files
COPY root/ /

ENTRYPOINT ["/init"]
