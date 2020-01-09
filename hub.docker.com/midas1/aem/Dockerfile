FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./atheneumd .
COPY ./atheneum-cli .

RUN chmod +x ./* && \
    ln atheneumd walletd && \
    ln atheneum-cli wallet-cli

VOLUME ["/root/.atheneum"]
EXPOSE 00000

RUN walletd --help || exit $(($? == 127))