FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./cryptoflowd .
COPY ./cryptoflow-cli .

RUN chmod +x ./* && \
    ln cryptoflowd walletd && \
    ln cryptoflow-cli wallet-cli

VOLUME ["/root/.cryptoflow"]
EXPOSE 3333

RUN walletd --help || exit $(($? == 127))
