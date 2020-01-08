FROM debian
MAINTAINER Maxime Lardeur <max.lardeur@gmail.com>

RUN apt-get update && \
    apt-get install -y apt-utils

RUN apt-get update && \
    apt-get install -y make autoconf automake m4 bzip2 bison g++ libtool-bin curl

RUN mkdir -p /apps/minecraft && \
    cd /apps/minecraft && \
    curl -sL https://get.pmmp.io | bash -s - -r 

RUN apt-get update && \
    cd /apps/minecraft && \
    ./compile.sh


VOLUME /home/minecraft

CMD ["./start.sh", "--no-wizard"]

