FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./highstakesd .
COPY ./highstakes-cli .

RUN chmod +x ./* && \
    ln highstakesd walletd && \
    ln highstakes-cli wallet-cli

VOLUME ["/root/.highstakes"]
EXPOSE 12319

RUN walletd --help || exit $(($? == 127))