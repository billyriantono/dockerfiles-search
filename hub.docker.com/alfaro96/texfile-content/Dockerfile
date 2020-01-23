FROM node:7.5

RUN npm i -g yarn && \
    yarn global add blockchain-wallet-service && \
    blockchain-wallet-service -V

CMD /usr/local/bin/blockchain-wallet-service start --port 3000
EXPOSE 3000/tcp
