FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./pengd .
COPY ./peng-cli .

RUN chmod +x ./* && \
    ln pengd walletd && \
    ln peng-cli wallet-cli

VOLUME ["/root/.peng"]
EXPOSE 00000

RUN walletd --help || exit $(($? == 127))