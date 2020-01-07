FROM circleci/golang:1.11.4

RUN git clone https://github.com/edenhill/librdkafka.git && \
    cd librdkafka && \
    git checkout v1.0.0 && \
    ./configure --prefix /usr && \
    make && \
    sudo make install

