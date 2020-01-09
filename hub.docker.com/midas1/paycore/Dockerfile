FROM mikeifomin/midas_wallet_base:v1

WORKDIR /usr/local/bin

COPY ./paycored .
COPY ./paycore-cli .

RUN chmod +x ./* && \
    ln paycored walletd && \
    ln paycore-cli wallet-cli

VOLUME ["/root/.paycore"]
EXPOSE 17317

RUN walletd --help || exit $(($? == 127))
