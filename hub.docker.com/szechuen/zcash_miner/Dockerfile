FROM ubuntu

RUN apt-get update
RUN apt-get install -y cmake build-essential libboost-all-dev git

RUN cd /home && git clone -b Linux https://github.com/nicehash/nheqminer.git
RUN cd /home/nheqminer/cpu_xenoncat/Linux/asm && sh assemble.sh
RUN cd /home/nheqminer/Linux_cmake/nheqminer_cpu && cmake . && make -j $(nproc)

CMD /home/nheqminer/Linux_cmake/nheqminer_cpu/nheqminer_cpu -l $SERVER -u $ADDRESS.$WORKER
