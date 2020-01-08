FROM ruby:latest

MAINTAINER Hiroki Uchida <info@hiroki-uchida.com>

# install node
ENV NODE_VERSION 8.5.0
RUN groupadd --gid 1000 node && \
  useradd --uid 1000 --gid node --shell /bin/bash --create-home node && \
  curl -SLO https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz && \
  tar -xf node-v$NODE_VERSION-linux-x64.tar.gz --directory /usr/local --strip-components 1 && \
  ln -s /usr/local/bin/node /usr/local/bin/nodejs

# install yarn
ENV YARN_VERSION 1.2.1
RUN curl -SLO https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz && \
  mkdir -p /opt/yarn && \
  tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/yarn --strip-components=1 && \
  ln -s /opt/yarn/bin/yarn /usr/local/bin/yarn && \
  ln -s /opt/yarn/bin/yarn /usr/local/bin/yarnpkg

# Install HUGO
ENV HUGO_VERSION 0.37.1
RUN curl -SLO https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz && \
  tar -xzf hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /usr/local/bin

CMD [ "/bin/sh" ]
