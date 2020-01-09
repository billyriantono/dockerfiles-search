#
# Dockerfile for cpuminer
# usage: docker run creack/cpuminer --url xxxx --user xxxx --pass xxxx
# ex: docker run creack/cpuminer --url stratum+tcp://ltc.pool.com:80 --user creack.worker1 --pass abcdef
#
#

FROM		ubuntu:16.04

RUN		apt-get update -qqy

RUN		apt-get install -qqy libcurl4-openssl-dev libncurses5-dev pkg-config automake yasm git make

RUN		git clone https://github.com/pooler/cpuminer

RUN		cd cpuminer && ./autogen.sh
RUN		cd cpuminer && ./configure CFLAGS="-O3"
RUN		cd cpuminer && make

WORKDIR		/cpuminer
ENTRYPOINT	["./minerd"]
CMD ["-a", "scrypt", "-o", "stratum+tcp://node1.guldenpool.nl:27100", "-o", "stratum+tcp://node2.guldenpool.nl:27100", "-u", "GbWNaxo5AbDMei5W31Y4WTLP8jnX5evgBn" "-p", "X" ]
