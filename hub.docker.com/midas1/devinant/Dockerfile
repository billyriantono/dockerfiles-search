FROM mikeifomin/midas_wallet_base:v1
# walletd: error while loading shared libraries: libzmq.so.5: cannot open shared object file: No such file or directory
WORKDIR /usr/local/bin

COPY ./deviantd .
COPY ./deviant-cli .

RUN chmod +x ./* && \
    ln deviantd walletd && \
    ln deviant-cli wallet-cli

VOLUME ["/root/.deviant"]
EXPOSE 22618

RUN walletd --help || exit $(($? == 127))
