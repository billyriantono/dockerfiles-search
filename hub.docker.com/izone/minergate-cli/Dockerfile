FROM ubuntu:xenial
MAINTAINER Leonardo Loures <luvres@hotmail.com>

## References:
# https://www.youtube.com/watch?v=lJY4XymBOOI
# https://github.com/OhGodAPet/cpuminer-multi
# https://minergate.com/altminers/cpuminer-multi-wolf

ENV USER="1uvr3z@gmail.com" \
	COIN=xmr \
	PORT=45560

RUN \
	apt-get update \
	&& apt-get install -y libcurl3-gnutls

COPY minerd /usr/bin

CMD minerd -a cryptonight -o stratum+tcp://$COIN.pool.minergate.com:$PORT -u $USER -p x
