# Pull base image.
FROM composer/composer:master-php5

# GPG keys listed at https://github.com/nodejs/node
RUN set -ex \
  && for key in \
    4ED778F539E3634C779C87C6D7062848A1AB005C \
    B9E2F5981AA6E0CD28160D9FF13993A75599653C \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    77984A986EBC2AA786BC0F66B01FBB92821C587A \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    A48C2BEE680E841632CD4E44F07496B3EB3C1762 \
    7937DFD2AB06298B2293C3187D33FF9D0246406D \
  ; do \
    gpg --keyserver pool.sks-keyservers.net --recv-keys "$key"; \
  done

ENV NODE_VERSION 10.11.0

RUN buildDeps='curl ca-certificates xz-utils phpunit' \
	&& set -x \
	&& apt-get update && apt-get install -y $buildDeps --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
	&& curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
	&& gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
	&& grep " node-v$NODE_VERSION-linux-x64.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
	&& tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
	&& rm "node-v$NODE_VERSION-linux-x64.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt

# Latest Git version
RUN echo "deb http://ftp.us.debian.org/debian testing main contrib non-free" >> /etc/apt/sources.list

# Install rsync for deployment
RUN apt-get remove binutils -y --force-yes && \ 
  apt-get update && \ 
  apt-get install -y --force-yes \
  openssh-client \
  rsync \
  bzip2 \
  python \
  libmcrypt-dev \
  php5-mcrypt \
  php5-mysql \
  php5-curl \
  git \
  && rm -r /var/lib/apt/lists/*

# Global install Gulp 4
RUN npm set progress=false && \
  npm install -g gulp@4.0.2

# Binary may be called nodejs instead of node
RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN apt-get purge -y --auto-remove $buildDeps

# Set correct entrypoint
CMD ["/bin/bash"]
ENTRYPOINT []