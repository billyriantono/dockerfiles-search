ARG NODE_VERSION_TARGET=10

FROM node:${NODE_VERSION_TARGET} as nodesrc

FROM jenkins/jnlp-slave

COPY --from=nodesrc /opt /opt
COPY --from=nodesrc /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=nodesrc /usr/local/share/doc/node /usr/local/share/doc/node
COPY --from=nodesrc /usr/local/share/systemtap/tapset/node.stp /usr/local/share/systemtap/tapset/node.stp
COPY --from=nodesrc /usr/local/include/node /usr/local/include/node
COPY --from=nodesrc /usr/local/bin/node /usr/local/bin/node

USER root
RUN ln -s /usr/local/bin/node /usr/local/bin/nodejs \
  ; ln -s /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
  ; ln -s /usr/local/lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx \
  ; ln -s `find /opt -name yarn -type f` /usr/local/bin/yarn \
  ; ln -s `find /opt -name yarnpkg -type f` /usr/local/bin/yarnpkg

USER jenkins

WORKDIR ${HOME}

LABEL maintainer="info@mjslabs.com"
