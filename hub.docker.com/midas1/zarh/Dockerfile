FROM mikeifomin/midas_wallet_base:v1-zeromq-dev

WORKDIR /usr/local/bin

COPY ./zarhexcashd .
COPY ./zarhexcash-cli .

RUN chmod +x ./* && \
    ln zarhexcashd walletd && \
    ln zarhexcash-cli wallet-cli

VOLUME ["/root/.zarhexcash"]
EXPOSE 55500

RUN walletd --help || exit $(($? == 127))