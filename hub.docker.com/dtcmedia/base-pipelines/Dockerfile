FROM ubuntu:18.04
### Adding source packages to apt lists, to manual build some packages
RUN grep '^deb ' /etc/apt/sources.list | \
  sed 's/^deb /deb-src /g' | \
  tee /etc/apt/sources.list.d/deb-src.list
### Update all core packages to latest version
RUN apt-get update -y && apt-get upgrade -y
RUN apt-get remove cmdtest

### Adding custom APT sources, to provide latest software versions
RUN apt-get install curl software-properties-common apt-transport-https sudo -y
RUN add-apt-repository -y ppa:git-ftp/ppa
RUN add-apt-repository -y ppa:ubuntu-toolchain-r/test
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh

### Manually rebuild CURL to allow SSL and SFTP support
RUN apt-get install -y build-essential debhelper libssh2-1-dev libssl-dev
RUN mkdir -p /opt/curl
RUN cd /opt/curl && apt source curl -y 
RUN cd /opt/curl && cd curl* && cd debian && sed -i -- "s/--without-ssl/--with-ssl --with-libssh2/g" rules
RUN cd /opt/curl && cd curl* && ./configure --with-ssl --with-libssh2 && make && make install
RUN rm /usr/bin/curl && ln -s /usr/local/bin/curl /usr/bin/curl
RUN apt-get autoremove -y
### Install aditional packages for Deployment environment
RUN export DEBIAN_FRONTEND=noninteractive && apt-get update && apt-get install -y unzip zip git-ftp nodejs php7.2 php7.2-mbstring php7.2-xml rsync yarn
RUN apt-get install php7.2-curl
RUN curl -sS "https://update.dtcmediainternet.nl/pipelines/dtcPipeline.sh" > /usr/local/bin/dtcPipeline && chmod a+x /usr/local/bin/dtcPipeline
RUN npm -g install eslint eslint-plugin-node eslint-plugin-standard eslint-plugin-promise eslint-config-standard eslint-plugin-import
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get clean
RUN php -v
RUN yarn --version
RUN nodejs -v
RUN curl -V
