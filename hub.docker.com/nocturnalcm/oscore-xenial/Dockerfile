FROM ubuntu:16.04
MAINTAINER "nocturnal coding monkeys,llc"

# ENVs
ENV TERM="xterm"
ENV LANG="C.UTF-8"
ENV LC_ALL="C.UTF-8"

# ARGs
ARG S6_OVERLAY_VERSION=v1.17.2.0
ARG DEBIAN_FRONTEND="noninteractive"
ARG BUILD_PACKAGES="automake build-essential"
ARG BASE_PACKAGES="tzdata iputils-ping traceroute perl bash "
# packages required by the BASE_PACKAGES
ARG BASE_PACKAGES_REQ="ca-certificates libffi6 libgdbm3 libgmp10 libgnutls-openssl27 libgnutls30 libhogweed4 libidn11 libnettle6 libp11-kit0 libperl5.22 libtasn1-6 perl-base perl-modules-5.22 "
# packages required to install the system
ARG TEMP_PACKAGES="curl"
# packages required by the TEMP_PACKAGES
ARG TEMP_PACKAGES_REQ="libasn1-8-heimdal libcurl3-gnutls libgssapi-krb5-2 libgssapi3-heimdal libhcrypto4-heimdal libheimbase1-heimdal libheimntlm0-heimdal libhx509-5-heimdal libk5crypto3 libkeyutils1 libkrb5-26-heimdal libkrb5-3 libkrb5support0 libldap-2.4-2 libroken18-heimdal librtmp1 libsasl2-2 libsasl2-modules-db libsqlite3-0 libwind0-heimdal"

RUN echo "**** updating APT ****" && \
    apt-get update && \
    echo "**** installing packages ****" && \
    apt-get install -y --no-install-recommends \
      ${BASE_PACKAGES} ${BASE_PACKAGES_REQ} ${TEMP_PACKAGES} ${TEMP_PACKAGES_REQ} && \
    #exit 99 && \
    echo "**** installing S6 ****" && \
    curl -J -L -o /tmp/s6-overlay-amd64.tar.gz https://github.com/just-containers/s6-overlay/releases/download/${S6_OVERLAY_VERSION}/s6-overlay-amd64.tar.gz && \
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && \
    echo "**** APT cleanup ****" && \
    apt-get -y remove ${TEMP_PACKAGES} ${TEMP_PACKAGES_REQ} && \
    apt-get -y autoremove && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    rm -rf /var/tmp/* && \
    echo "**** finished basic package install ****"

RUN echo "<**** adding coreuser user acount & group ****>" && \
    addgroup --gid 1000 coreuser && \
    adduser --home "/coreuser" --gid 1000 --uid 1000  --disabled-password --shell "/bin/bash" --gecos "" coreuser && \
    echo "</**** adding coreuser user acount & group ****>"


# COPY files to be part of this image.
COPY root/ /


# ENTRYPOINT
ENTRYPOINT ["/"]

# EXPOSE ports
# EXPOSE

# VOLUMEs
# VOLUME
