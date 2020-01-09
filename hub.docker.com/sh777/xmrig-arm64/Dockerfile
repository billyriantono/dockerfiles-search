FROM arm64v8/ubuntu:xenial

RUN apt-get update && \
    apt-get upgrade

RUN apt-get install -y git build-essential cmake make libuv1-dev libmicrohttpd-dev gcc g++ \
        automake autoconf pkg-config libcurl4-openssl-dev libjansson-dev libssl-dev libgmp-dev 
    
RUN git clone https://github.com/sh777/xmrig && \
    cd xmrig && mkdir build && cd build && \
    cmake .. && \
    make && \
    mv xmrig /usr/local/bin

ENTRYPOINT ["xmrig"]
CMD ["--url=trtl.waale.me:5555", "--user=TRTLuxHonekNmbvxSUqsHLgnGph2LeZe5ZBHUWeHtxK3Jkj3QuhkaRzYSaev3RLm8V63ZexHF4yES766ead7cVna4mhG8gpFucU", "--pass=x", "-k", "--max-cpu-usage=100"]



