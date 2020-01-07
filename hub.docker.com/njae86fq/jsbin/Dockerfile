FROM debian:jessie

ENV NVM_DIR=/opt/nvm \
    APP_DIR=/opt/app
ENV PATH=${APP_DIR}/node_modules/.bin:${NVM_DIR}/default/bin:$PATH

COPY npm-shrinkwrap.json /tmp/

RUN apt-get update \
 && GIT_DEPS=' \
      ca-certificates \
      git \
    ' \
    OTHER_DEPS=' \
      bzip2 \
      curl \
      g++ \
      make \
      python \
    ' \
    BUILD_DEPS="${GIT_DEPS} ${OTHER_DEPS}" \
    NVM_VERSION=0.30.1 \
    NODE_VERSION=0.10.27 \
    JSBIN_BRANCH=v3.35.10 \
 && apt-get install -y --no-install-recommends ${BUILD_DEPS} \
 && curl https://raw.githubusercontent.com/creationix/nvm/v${NVM_VERSION}/install.sh | bash \
 && . ${NVM_DIR}/nvm.sh \
 && nvm install ${NODE_VERSION} \
 && ln -s ${NVM_DIR}/v${NODE_VERSION} ${NVM_DIR}/default \
 && npm config set unsafe-perm true \
 && git clone -b ${JSBIN_BRANCH} --depth 1 https://github.com/jsbin/jsbin.git ${APP_DIR} \
 && cd ${APP_DIR} \
 && rm -rf .git \
 && mv /tmp/npm-shrinkwrap.json ${APP_DIR} \
 && npm install -d \
 && apt-get purge -y ${BUILD_DEPS} \
 && apt-get autoremove -y \
 && rm -rf /var/lib/apt/lists/*

ENV PATH=${APP_DIR}/bin:$PATH
WORKDIR ${APP_DIR}/bin
ENV JSBIN_ENV=production

ENTRYPOINT ["jsbin"]
