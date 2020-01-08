FROM nvidia/cuda:9.0-base
MAINTAINER Leonardo Loures <luvres@hotmail.com>

## References:
# https://minergate.com/altminers/ewbf-cuda-btg
# https://github.com/poolgold/ewbf-miner-btg-edition/releases

ENV \
	POOL="eu1-zcash.flypool.org" \
	PORT="3333" \
	USER="t1UuXA2PPFHjzJJ4xjrUE4WkzAZp4HyNims.1uvr3z"

COPY miner /usr/bin

CMD miner --server $POOL --port $PORT --user $USER   --pass x --cuda_devices 0
