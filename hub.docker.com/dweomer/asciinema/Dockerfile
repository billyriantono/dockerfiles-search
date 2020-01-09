ARG ALPINE=golang:alpine
FROM ${ALPINE}
RUN set -x \
 && apk add --no-cache \
    bash \
    bc \
    coreutils \
    gawk \
    git \
    grep \
    less \
    ncurses \
    py3-pip \
    sed \
    vim \
 && pip3 install asciinema \
 && asciinema --version \
 && go version
 COPY export-*.sh /etc/profile.d/
 WORKDIR /usr/local
 CMD ["bash","--login"]
 