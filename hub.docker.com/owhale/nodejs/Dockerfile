FROM owhale/base:latest
LABEL maintainer="Bluewhale <blue@owhale.com>"

# nodejs
RUN mkdir -p /usr/local/nvm
ENV NVM_DIR /usr/local/nvm
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | zsh && \
    . $NVM_DIR/nvm.sh && \
    nvm install --lts

# yarn
RUN . $NVM_DIR/nvm.sh && \
    npm install -g yarn

# pm2
RUN . $NVM_DIR/nvm.sh && \
    yarn global add pm2

WORKDIR /root
CMD /bin/zsh
