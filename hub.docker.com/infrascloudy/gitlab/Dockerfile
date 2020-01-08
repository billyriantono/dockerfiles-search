FROM ubuntu:xenial
MAINTAINER dragonmaster <support@linaccess.za.net>

# Install required packages
RUN apt-get update -q
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
    ca-certificates openssh-server wget apt-transport-https vim-nox nano \
    letsencrypt curl postfix

# Adding GitLab package server and install the package
COPY script.deb.sh /
RUN bash /script.deb.sh
RUN apt install gitlab-ce -y
# RUN gitlab-ctl reconfigure
RUN gitlab-ctl restart
