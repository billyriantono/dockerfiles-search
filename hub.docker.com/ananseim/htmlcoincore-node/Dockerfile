FROM ananseim/htmlcoincore-deps
#LABEL maintainer="https://github.com/senagbe"

RUN npm install -g htmlcoincore-node

RUN mkdir /home/node/mynode-data

RUN htmlcoincore-node create -d /home/node/mynode-data /home/node/mynode
WORKDIR /home/node/mynode
RUN htmlcoincore-node install htmlcoin-api
COPY htmlcoincore-node.json /home/node/mynode/htmlcoincore-node.json
COPY htmlcoin.conf /home/node/mynode/htmlcoin.conf

ENTRYPOINT ["htmlcoincore-node", "start", "-c", "/home/node/mynode"]