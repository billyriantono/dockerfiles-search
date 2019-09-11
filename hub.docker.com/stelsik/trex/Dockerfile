FROM debian:buster AS TRex

LABEL RUN docker run --privileged --cap-add=ALL -v /mnt/huge:/mnt/huge -v /lib/modules:/lib/modules:ro -v /sys/bus/pci/devices:/sys/bus/pci/devices -v /sys/devices/system/node:/sys/devices/system/node -v /dev:/dev --name NAME -e NAME=NAME -e IMAGE=IMAGE IMAGE

COPY trex_cfg.yaml /etc/trex_cfg.yaml

RUN apt-get update
RUN apt-get install -y sudo gcc g++ python git zlib1g-dev pciutils vim kmod strace wget mc

RUN git clone https://github.com/cisco-system-traffic-generator/trex-core.git 

RUN cd /trex-core/linux_dpdk && \
    ./b configure && \
    ./b install

RUN cd /trex-core/linux && \
    ./b configure && \
    ./b install

WORKDIR /trex-core

CMD ["/bin/bash"]
