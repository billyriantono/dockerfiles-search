FROM atlassian/bamboo-agent-base:6.8.1

ENV NODE_VERSION=10.15.3

ENV NVM_NODEJS_ORG_MIRROR=http://npm.taobao.org/mirrors/node
ENV NVM_DIR=$BAMBOO_USER_HOME/.nvm

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

# install nvm
# https://github.com/creationix/nvm#install-script
RUN mkdir -p ${NVM_DIR} && \
  wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash && \
  npm install -g yarn

RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.builder.node.Node.js" "$NVM_DIR/versions/node/v$NODE_VERSION/bin/node"
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.builder.node.npm" "$NVM_DIR/versions/node/v$NODE_VERSION/bin/npm"
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.builder.node.yarn" "$NVM_DIR/versions/node/v$NODE_VERSION/bin/yarn"
