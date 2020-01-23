#
# Base image
#

FROM    centos:6 AS base
RUN     yum -y update && \
        yum install -y openssl 


################################################################################

#
# Base-build image
#

FROM    base AS builder

ARG     BUILD_DATE
ARG     SOURCE_REPOSITORY_URL
ARG     SOURCE_COMMIT

LABEL   org.opencontainers.image.title="Build-Base" \
        org.opencontainers.image.description="A base CENTOS 6 image with development tools installed to build software." \
        org.opencontainers.image.created=$BUILD_DATE \
        org.opencontainers.image.source=$SOURCE_REPOSITORY_URL \
        org.opencontainers.image.revision=$SOURCE_COMMIT

WORKDIR /

RUN     set -ex ; \
        yum --enablerepo=extras install -y epel-release ; \
        yum groupinstall "Development tools" -y 


################################################################################

#
# Service Base State
#

FROM    base AS server

ARG     BUILD_DATE
ARG     SOURCE_REPOSITORY_URL
ARG     SOURCE_COMMIT

LABEL   org.opencontainers.image.title="Service-Base" \
        org.opencontainers.image.description="A base CENTOS 6 image with minimal installed." \
        org.opencontainers.image.created=$BUILD_DATE \
        org.opencontainers.image.source=$SOURCE_REPOSITORY_URL \
        org.opencontainers.image.revision=$SOURCE_COMMIT

RUN     yum -y install epel-release && \
        rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6


################################################################################

#
# Build rpm builder
#

FROM    builder AS rpm-builder

ARG     BUILD_DATE
ARG     SOURCE_REPOSITORY_URL
ARG     SOURCE_COMMIT

LABEL   org.opencontainers.image.title="RPM-Build-Base" \
        org.opencontainers.image.description="A base CENTOS 6 image for building RPM packages." \
        org.opencontainers.image.created=$BUILD_DATE \
        org.opencontainers.image.source=$SOURCE_REPOSITORY_URL \
        org.opencontainers.image.revision=$SOURCE_COMMIT

WORKDIR /root

RUN     BUILD_TOOLS="libtool autoconf pkgconfig automake rpmdevtools rpmlint yum-utils" && \
        BUILD_DEPS="gnutls30-devel libidn-devel libgsasl-devel gettext" && \
        yum install -y ${BUILD_TOOLS} ${BUILD_DEPS}

ONBUILD RUN \
        set -ex ; \
        rpmdev-setuptree ; \
        echo '%_libdir32  %{_prefix}/lib' >> ${HOME}/.rpmmacros

