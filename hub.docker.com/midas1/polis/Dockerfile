FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./polisd .
COPY ./polis-cli .

RUN chmod +x ./* && \
    ln polisd walletd && \
    ln polis-cli wallet-cli

VOLUME ["/root/.polis"]
EXPOSE 24126

RUN walletd --help || exit $(($? == 127))