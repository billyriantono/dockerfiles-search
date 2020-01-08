FROM openjdk:8

RUN apt-get update && apt-get install build-essential -y && \
  curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

ENV NVM_DIR="$HOME/.nvm"
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN /bin/bash -c "source /root/.bashrc && nvm install v8.1.4 && nvm use node"