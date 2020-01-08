FROM centos:7
MAINTAINER Steven J. McDowall <steve@accendi.com>

ARG MARIA_VERSION=10.1

# Copy only files required for the following RUN commands (leverage Docker caching)
COPY rootfs/etc/yum.repos.d/MariaDB.repo /etc/yum.repos.d

RUN \
    sed -i s:MARIA_VERSION:$MARIA_VERSION: /etc/yum.repos.d/MariaDB.repo \
    && yum update -y \
    && yum install -y epel-release \
    && yum install -y --setopt=tsflags=nodocs \
        MariaDB-server \
        hostname \
        net-tools \
        pwgen  \
    && yum -y clean all \
    && rm -rf /var/lib/mysql/*

# Now copy everything else over..
COPY rootfs /

# Add VOLUME to allow backup of data
VOLUME ["/var/lib/mysql"]

# Set TERM env to avoid mysql client error message "TERM environment variable not set" when running from inside the container
ENV TERM xterm

EXPOSE 3306
CMD ["/run.sh"]
