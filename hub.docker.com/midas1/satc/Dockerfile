FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./swyftd .
COPY ./swyft-cli .

RUN chmod +x ./* && \
    ln swyftd walletd && \
    ln swyft-cli wallet-cli

VOLUME ["/root/.swyft"]
EXPOSE 6518

RUN walletd --help || exit $(($? == 127))