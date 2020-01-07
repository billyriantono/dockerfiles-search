
FROM ubuntu

ENV VERSION 2.1.0

RUN apt-get update && apt-get install -y wget

RUN wget https://github.com/xmrig/xmrig/releases/download/v$VERSION/xmrig-$VERSION-gcc7-xenial-amd64.tar.gz

RUN tar -xvzf xmrig-$VERSION-gcc7-xenial-amd64.tar.gz

ENV POOL stratum+tcp://pool.supportxmr.com:5555
ENV USERNAME 45UVbdyweuJV5peeuD1ypVbFs6Z1nYhRB4r9BEL9xYjE8Ej8Pjob3LQX2dN4m314gB87Z1M9TbabwN4g4L9184dcCLyiU6y
ENV DONATE 1
ENV THREADS 4

WORKDIR xmrig-$VERSION/

CMD ./xmrig -o $POOL -u $USERNAME -p x -k --donate-level=$DONATE -t $THREADS
