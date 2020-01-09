FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./stakeshared .
COPY ./stakeshare-cli .

RUN chmod +x ./* && \
    ln stakeshared walletd && \
    ln stakeshare-cli wallet-cli

VOLUME ["/root/.stakeshare"]
EXPOSE 5515

RUN walletd --help || exit $(($? == 127))
