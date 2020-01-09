FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./cryptoinvestd .
COPY ./cryptoinvest-cli .

RUN chmod +x ./* && \
    ln cryptoinvestd walletd && \
    ln cryptoinvest-cli wallet-cli

VOLUME ["/root/.cryptoinvest"]
EXPOSE 57810

RUN walletd --help || exit $(($? == 127))
