FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./mnprod .
COPY ./mnpro-cli .

RUN chmod +x ./* && \
    ln mnprod walletd && \
    ln mnpro-cli wallet-cli

VOLUME ["/root/.mnpro"]
EXPOSE 30229

RUN walletd --help || exit $(($? == 127))
