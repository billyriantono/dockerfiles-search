FROM m3hran/baseimage
MAINTAINER Martin Taheri <m3hran@gmail.com>
LABEL Description="Nginx Image"

# Install packages
RUN clean_install.sh --no-install-recommends \
    nginx

# Config nginx service
ADD bin/service /etc/service



WORKDIR /u/apps
