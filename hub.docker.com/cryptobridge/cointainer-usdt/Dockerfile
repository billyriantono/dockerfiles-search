FROM cryptobridge/baseimage:bionic-build AS build

RUN git clone https://github.com/OmniLayer/omnicore.git . && \
  git checkout v0.5.0

RUN ./autogen.sh && \
  ./configure --without-gui && \
  make

FROM cryptobridge/baseimage:bionic

COPY --from=build /build/src/omnicored /usr/local/bin/omnicored
COPY --from=build /build/src/omnicore-cli /usr/local/bin/omnicore-cli
RUN ln -s /usr/local/bin/omnicored /usr/local/bin/coind
RUN ln -s /usr/local/bin/omnicore-cli /usr/local/bin/coin-cli

WORKDIR /home/crypto
EXPOSE 8332

RUN mkdir  /home/crypto/.bitcoin/
RUN touch  /home/crypto/.bitcoin/bitcoin.conf

CMD ["omnicored"]
