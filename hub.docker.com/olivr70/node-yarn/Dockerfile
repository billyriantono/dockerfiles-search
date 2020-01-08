FROM node:9.3-slim

ENV NODE_VER=9.3
ENV YARN_VER=1.3.2
LABEL node=$NODE_VER
LABEL yarn=$YARN_VER

MAINTAINER Olivier Chevet <olivr70@outlook.fr>

# Global install yarn package manager
# RUN wget -qO- https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --import \
  # && wget https://yarnpkg.com/latest.tar.gz -P /tmp/yarn \
  # && wget https://yarnpkg.com/latest.tar.gz.asc -P /tmp/yarn \
  # && gpg --verify /tmp/yarn/latest.tar.gz.asc \
  # && mkdir -p $HOME/.yarn \
  # && tar zvxf /tmp/yarn/latest.tar.gz -C $HOME/.yarn --strip-components=1 \
  # && export PATH=$HOME/.yarn/bin:$PATH \
  # && rm /tmp/yarn/latest.tar.* \
  # && rmdir /tmp/yarn
COPY yarn-install.sh /tmp
RUN chmod +x /tmp/yarn-install.sh
RUN /tmp/yarn-install.sh

# ------------ packages ------------
COPY packages.sh /tmp
RUN chmod +x /tmp/packages.sh
RUN /tmp/packages.sh

WORKDIR /workspace