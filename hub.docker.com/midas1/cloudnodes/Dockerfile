FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./cloudnodesd .
COPY ./cloudnodes-cli .

RUN chmod +x ./* && \
    ln cloudnodesd walletd && \
    ln cloudnodes-cli wallet-cli

VOLUME ["/root/.cloudnodes"]
EXPOSE 8173

RUN walletd --help || exit $(($? == 127))
