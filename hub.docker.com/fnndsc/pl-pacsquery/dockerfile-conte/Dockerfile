FROM ubuntu:xenial
MAINTAINER Filipe Manco <filipe.manco@gmail.com>

ENV hugo_version=0.20.7
ENV hugo_deb=hugo_${hugo_version}_Linux-64bit.deb
ENV hugo_deb_url=https://github.com/spf13/hugo/releases/download/v${hugo_version}/${hugo_deb}

# Upgrade
RUN apt-get update && apt-get -y upgrade -u && apt-get clean

# Install git and ssh client to retrieve sources
RUN apt-get install -y --no-install-recommends openssh-client git

# Install hugo
ADD ${hugo_deb_url} /tmp/hugo.deb
RUN dpkg -i /tmp/hugo.deb && rm -f /tmp/hugo.deb

CMD ["/bin/bash"]
