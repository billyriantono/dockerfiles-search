FROM hyperledger/composer-rest-server
RUN npm install -g @ampretia/composer-wallet-cloudant && \
    npm cache clean --force && \
    ln -s node_modules .node_modules

