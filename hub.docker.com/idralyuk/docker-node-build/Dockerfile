FROM node:8.9.0

RUN curl -fsSL get.docker.com |sh && \
  apt-get install -y python-dev python-yaml python-pip && \
  pip install awscli && \
  apt-get autoremove && \
  apt-get clean && \
  npm install npm@5.2.0 && \
  rm -rf /usr/local/lib/node_modules/npm && \
  mv node_modules/npm /usr/local/lib/node_modules/npm && \
  npm install -g nyc
