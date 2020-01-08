FROM ubuntu:16.04

WORKDIR /root
RUN apt-get update && apt-get install -y libreadline-dev libconfig-dev libssl-dev lua5.2 liblua5.2-dev libevent-dev libjansson-dev libpython-dev make
RUN apt-get update && apt-get install -y git-core
RUN git clone --recursive https://github.com/vysheng/tg.git

WORKDIR /root/tg
RUN ./configure
RUN make

RUN apt-get update && apt-get install -y vim
RUN apt-get update && apt-get install -y iptables ufw ruby
RUN echo "set input-meta on\nset output-meta on\nset convert-meta off" >/root/.inputrc

CMD bash
