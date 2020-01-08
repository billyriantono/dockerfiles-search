from node:10

env DEBIAN_FRONTEND=noninteractive \
  SUDO_FORCE_REMOVE=yes

run sed -i "/deb-src/d" /etc/apt/sources.list && \
  npm install -g ember-cli && \
  apt-get update && apt-get install -yq sudo python-dev && \
  git clone https://github.com/facebook/watchman.git /watchman && \
  cd /watchman && git checkout v4.9.0 && \
 ./autogen.sh && ./configure && make && make install && \
 apt-get purge -yq sudo && rm -rf /watchman /var/lib/apt/lists/*
