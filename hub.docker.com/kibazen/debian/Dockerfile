# vim:set ft=dockerfile:
FROM debian:stable


# system tools
RUN set -ex \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends apt-utils \
    && rm -rf /var/lib/apt/lists/*

# make the "en_US.UTF-8" locale
RUN set -ex \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends locales \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

# common tools
RUN set -ex \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        # security tools
        ca-certificates gnupg dirmngr openssl openssh-client \
        # develop tools
        autoconf automake binutils make file patch \
        # network tools
        curl wget netcat-openbsd \
        # other tools
        vim less bzip2 xz-utils procps \
    && rm -rf /var/lib/apt/lists/*