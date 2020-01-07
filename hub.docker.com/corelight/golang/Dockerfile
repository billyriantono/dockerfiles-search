FROM golang:1

RUN curl -L -O https://github.com/mitchellh/golicense/releases/download/v0.1.1/golicense_0.1.1_linux_x86_64.tar.gz &&\
    mkdir tmp &&\
    tar -xzf golicense_0.1.1_linux_x86_64.tar.gz -C tmp &&\
    mv tmp/golicense /usr/local/bin/golicense &&\
    rm -rf tmp &&\
    rm golicense_0.1.1_linux_x86_64.tar.gz
