FROM docker.io/centos:7

# Set the Gitea Version to install.
# Check https://dl.gitea.io/gitea/ for available versions.
RUN yum -y update && yum -y upgrade \
    && yum -y install git asciidoc ca-certificates \
              gettext openssh s6 su-exec tzdata cronie nano unzip \
    && yum -y clean all \
    && yum -y install zip \
    && yum -y install unzip \
    && rm -rf /var/cache/yum
