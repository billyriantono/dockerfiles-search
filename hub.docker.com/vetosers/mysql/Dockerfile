#####################################################
# Dockerfile to customeize PHP for Laravel project
# Based on the official MySQL
#####################################################

# Set the base image
FROM        mysql:5.7

# File Author / Maintainer
LABEL       maintainer=vetosers@gmail.com

# Environmental Variables
ARG         DEBIAN_FRONTEND=noninteractive

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
                rsync \
            && apt-get autoremove -fy \
            && apt-get clean \
            && apt-get autoclean -y \
            && rm -rf /var/lib/apt/lists/*

# Configurations
COPY        conf.d /etc/mysql/conf.d
