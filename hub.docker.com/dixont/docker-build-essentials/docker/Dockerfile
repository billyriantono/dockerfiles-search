FROM trufflesuite/ganache-cli:v6.4.3

WORKDIR /testchain

COPY . .
RUN apk add tar && mkdir chaindata && tar xzf ./snapshots/MKR-WITH-TX_MANAGER.tgz -C ./chaindata

EXPOSE 2000

ENTRYPOINT ["node", "/app/ganache-core.docker.cli.js", "-m", "hill law jazz limb penalty escape public dish stand bracket blue jar", "--db", "chaindata", "-p", "2000"]
