FROM nginx:alpine

RUN apk add --no-cache libstdc++ ca-certificates openssl &&\
    apk add --no-cache --virtual .build-deps \
        binutils-gold \
        curl \
        g++ \
        gcc \
        gnupg \
        libgcc \
        linux-headers \
        make \
        python


RUN wget https://nodejs.org/download/release/v6.12.2/node-v6.12.2.tar.gz &&\
    tar xzfv node-v6.12.2.tar.gz && \
    cd node-v6.12.2 &&\
    ./configure &&\
    make -j4 && \
    make install

#RUN apk del libstdc++ ca-certificates openssl gcc g++ clang linux-headers make python &&\
#    rm -rf /var/cache/apk/*

RUN npm install -g @angular/cli@1.3.1

RUN mkdir /app-src

COPY compilar.sh /tmp/compilar.sh

RUN chmod 0744 /tmp/compilar.sh

WORKDIR /app-src

CMD ["ash", "/tmp/compilar.sh"]