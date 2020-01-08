#####################################################
# Dockerfile to customeize Python for GitLab Deployment
# Based on the official Python
#####################################################

# Set the base image
FROM        python:2.7

# File Author / Maintainer
LABEL       maintainer=vetosers@gmail.com

# Change System TimeZone to Asia/Bangkok
RUN         ln -sf /usr/share/zoneinfo/Asia/Bangkok /etc/localtime

# Update Repositories
RUN         apt-get update --fix-missing \
            && apt-get upgrade -fy \
            && apt-get dist-upgrade -fy \
            && apt-get install --no-install-recommends -fy \
                autoconf \
                pkg-config \
                apt-utils \
                apt-transport-https \
                git \
                wget \
                zlib1g-dev \
                build-essential \
                autoconf \
                libtool \
                pkg-config \
                libxml2-dev \
                libxslt-dev \
                python-dev \
                libsasl2-dev \
                python-dev \
                libldap2-dev \
                libssl-dev \
            && apt-get autoremove -fy \
            && apt-get clean \
            && apt-get autoclean -y \
            && rm -rf /var/lib/apt/lists/*
            