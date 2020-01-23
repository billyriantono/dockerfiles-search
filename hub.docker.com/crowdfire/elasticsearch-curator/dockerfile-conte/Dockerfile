FROM ubuntu:18.04
RUN set -x
RUN apt-get update -q && apt-get -y -q upgrade
RUN apt-get install -y -q git wget
RUN apt-get install -y -q cmake g++
RUN apt-get install -y -q libmicrohttpd-dev libssl-dev libhwloc-dev 
RUN apt-get install -y -q linux-source
RUN export CUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda

ARG CUDA=OFF

WORKDIR /tmp/
ADD build_xmr-stak_docker_layer.sh ./
RUN ./build_xmr-stak_docker_layer.sh && rm -rf build_xmr-stak_docker_layer.sh

# an external config.txt file must be mapped to /usr/local/src/xmr-stak/config.txt
# Example: if config.txt is on current folder, map a volume like:
# ${PWD}/config.txt:/usr/local/src/xmr-stak/config.txt

WORKDIR /usr/local/src/xmr-stak
CMD ./xmr-stak

