FROM debian:stretch-slim
ARG DEBIAN_FRONTEND=noninteractive

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV BASH_ENV=/etc/profile
WORKDIR /tmp/

ARG CONTAINER_RUNTIME_REQUIREMENTS="less procps ca-certificates"
ARG CONTAINER_RUNTIME_REQUIREMENTS_EXTRA=""
ARG CONTAINER_BUILD_REQUIREMENTS="curl"
ARG CONTAINER_BUILD_REQUIREMENTS_EXTRA=""

COPY FS /

# hadolint ignore=DL3008,DL3015
RUN set -Eeu; \
    chmod 755 /usr/local/bin/{docker-layer-clean,docker-install-requirements,docker-package-download}; \
    \
        ## add debian stretch backports repo
    	{ \
    		echo 'Package: *'; \
    		echo 'Pin: release n=stretch-backports'; \
    		echo 'Pin-Priority: 500'; \
    	} > /etc/apt/preferences.d/stretch-backports_default; \
    	{ \
    		echo 'deb http://http.debian.net/debian stretch-backports main contrib non-free'; \
    	} > /etc/apt/sources.list.d/stretch-backports.list; \
    echo "alias ll=\"ls -lisah\"" >> ~/.bashrc; \
    echo "export PATH=\"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin\"" > /etc/environment; \
    echo "APT::Install-Recommends \"false\";" > /etc/apt/apt.conf.d/docker-disable-recommends; \
    mkdir -p /usr/share/man/man1; \
    mkdir -p /usr/share/man/man7; \
    /usr/local/bin/docker-install-requirements; \
    /usr/local/bin/docker-layer-clean