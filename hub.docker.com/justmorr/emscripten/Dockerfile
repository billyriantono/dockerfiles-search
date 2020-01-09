FROM alpine

RUN apk upgrade && apk add git python3

RUN git clone https://github.com/emscripten-core/emsdk.git

WORKDIR /emsdk

RUN git pull && \
    ./emsdk install latest && \
    ./emsdk activate latest

ENTRYPOINT [ "./emsdk" ]
