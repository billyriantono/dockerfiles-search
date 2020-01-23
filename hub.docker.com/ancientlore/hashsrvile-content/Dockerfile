FROM ananseim/htmlcoincore-node
#LABEL maintainer="https://github.com/senagbe"

USER root
RUN chown node:node /home/node/mynode/htmlcoincore-node.json && \
    chmod 777 /home/node/mynode/htmlcoincore-node.json
USER node

RUN htmlcoincore-node install htmlcoin-explorer
RUN htmlcoincore-node install htmlcoin-notification

COPY htmlcoincore-node.json /home/node/mynode/htmlcoincore-node.json

ENTRYPOINT ["htmlcoincore-node", "start", "-c", "/home/node/mynode"]