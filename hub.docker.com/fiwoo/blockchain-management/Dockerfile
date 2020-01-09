FROM ubuntu:16.04

WORKDIR /opt/

COPY * /opt/

RUN apt update
RUN apt-get update
RUN apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:ethereum/ethereum 
RUN apt-get update
RUN apt-get install -y build-essential unzip libdb-dev libleveldb-dev libsodium-dev zlib1g-dev libtinfo-dev solc sysvbanner wrk -y
RUN apt-get install ethereum -y

RUN apt-get install nano -y

RUN apt update
RUN apt install wget -y
RUN wget -q https://github.com/jpmorganchase/constellation/releases/download/v0.3.2/constellation-0.3.2-ubuntu1604.tar.xz
RUN tar xfJ constellation-0.3.2-ubuntu1604.tar.xz
RUN cp constellation-0.3.2-ubuntu1604/constellation-node /usr/local/bin && chmod 0755 /usr/local/bin/constellation-node
RUN rm -rf constellation-0.3.2-ubuntu1604

RUN add-apt-repository ppa:gophers/archive -y
RUN apt update
RUN apt-get install golang-1.9-go -y
RUN PATH=$PATH:/usr/lib/go-1.9/bin

RUN apt-get install git -y

RUN git clone https://github.com/jpmorganchase/quorum.git

CMD python N.py $Var1 $Var2; cd quorum; PATH=$PATH:/usr/lib/go-1.9/bin; make all; cp build/bin/geth /usr/local/bin; cp build/bin/bootnode /usr/local/bin; cd -;sh 1-create.sh; sh 2-constellation.sh; sh 3-start.sh;export set Var1=;export set Var2=;


EXPOSE 9001 22000 21000 50401 30303 30303/udp 30304/udp


