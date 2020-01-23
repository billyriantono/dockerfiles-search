FROM google/cloud-sdk:latest

ENV NPM_TOKEN ''
ENV NODE_VERSION 10.15.1
ENV NVM_DIR /usr/local/nvm
ENV PATH ${NVM_DIR}/versions/node/v${NODE_VERSION}/bin:${PATH}
ENV NODE_PATH=${NVM_DIR}/v${NODE_VERSION}/lib/node_modules

RUN pip install awscli==1.16.177 gitpython requests --user
RUN mkdir -p ${NVM_DIR} && curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

RUN /bin/bash -c "source ${NVM_DIR}/nvm.sh \
  && nvm install ${NODE_VERSION} \
  && nvm alias default ${NODE_VERSION} \
  && nvm use default"
