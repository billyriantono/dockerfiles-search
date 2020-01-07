FROM debian:latest
MAINTAINER Rostislav Postrednik http://postrednik.cz

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -y \
        curl \
        sudo \
        git \
        build-essential \
        graphicsmagick \
        libssl-dev \
        libpng-dev

ENV NVM_DIR /usr/local/.nvm
ENV NODE_VERSION 5.6.0

# Install nvm
RUN git clone https://github.com/creationix/nvm.git $NVM_DIR && \
    cd $NVM_DIR && \
    git checkout `git describe --abbrev=0 --tags`

COPY scripts/ /root/scripts/

# Install default version of Node.js
RUN chmod +x /root/scripts/nvm-install.sh && /root/scripts/nvm-install.sh && rm -Rf /root/scripts/

# Add nvm.sh to .bashrc for startup...
RUN echo "source ${NVM_DIR}/nvm.sh" > $HOME/.bashrc && \
    source $HOME/.bashrc

# ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
# ENV PATH      $NVM_DIR/v$NODE_VERSION/bin:$PATH

# Install meteor
RUN curl -sL https://install.meteor.com | sed s/--progress-bar/-sL/g | /bin/sh

# Install rvm & ruby
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \
    \curl -sSL https://get.rvm.io | bash -s stable --ruby
    