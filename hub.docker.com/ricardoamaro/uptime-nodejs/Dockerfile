FROM ricardoamaro/uptime-base:latest

MAINTAINER Ricardo Amaro <ricardo.amaro_at_acquia.com>
ENV DEBIAN_FRONTEND noninteractive

# Install Python
RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*

# Install Node.js
RUN \
  cd /tmp && \
  wget http://nodejs.org/dist/node-latest.tar.gz && \
  tar xvzf node-latest.tar.gz && \
  rm -f node-latest.tar.gz && \
  cd node-v* && \
  ./configure && \
  CXX="g++ -Wno-unused-local-typedefs" make && \
  CXX="g++ -Wno-unused-local-typedefs" make install && \
  cd /tmp && \
  rm -rf /tmp/node-v* && \
  npm install -g npm && \
  printf '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc

# Install config
RUN mkdir /root/.ssh
COPY ./files/config /root/.ssh/config
RUN chmod 600 -R /root/.ssh

# Install start
COPY ./files/start.sh /start.sh
RUN chmod 755 /start.sh

# Define working directory.
WORKDIR /data

EXPOSE 80
# Define default command.
CMD ["/bin/bash", "/start.sh"]
