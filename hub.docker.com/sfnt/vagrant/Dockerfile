FROM ubuntu:bionic
ENV VERSION=2.2.3 \
    PLUGIN_VER=0.3.2
RUN apt-get update && apt-get -y install ruby-dev curl ftp python-pip
RUN curl -o vagrant_${VERSION}_x86_64.deb \
    https://releases.hashicorp.com/vagrant/${VERSION}/vagrant_${VERSION}_x86_64.deb && \
    dpkg --install vagrant_${VERSION}_x86_64.deb && rm -f vagrant_${VERSION}_x86_64.deb
RUN vagrant plugin install vagrant-vcenter --plugin-version ${PLUGIN_VER}
