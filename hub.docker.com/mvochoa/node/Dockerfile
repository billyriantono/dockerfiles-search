FROM ubuntu:14.04

USER root

ENV HOME /root
ENV NVM_DIR $HOME/.nvm
ENV NODE_VERSION 6.14.3
ENV PATH ${NVM_DIR}/versions/node/v${NODE_VERSION}/bin:${PATH}

RUN apt-get update && apt-get install -y build-essential libssl-dev zip git curl
RUN git clone https://github.com/creationix/nvm.git "$NVM_DIR" \
    && cd "$NVM_DIR" && git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)` \
    && . $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && npm config set user 0 \
    && npm config set unsafe-perm true

RUN echo "export NVM_DIR=\"$HOME/.nvm\"" >> $HOME/.bashrc
RUN echo "[ -s \"$NVM_DIR/nvm.sh\" ] && \. \"$NVM_DIR/nvm.sh\"" >> $HOME/.bashrc
RUN echo "[ -s \"$NVM_DIR/bash_completion\" ] && \. \"$NVM_DIR/bash_completion\"" >> $HOME/.bashrc
