FROM ufoym/deepo:pytorch-py36

RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get -y update && \
    apt-get -y install nfs-common cifs-utils sshpass wget git graphviz openssh-server openssh-client curl zip fuse golang
RUN python3 -m pip install --upgrade pip
RUN python3 -m pip --no-cache-dir install torchvision tb-nightly tensorboardx pyyaml graphviz hdfs
RUN git clone --recursive https://github.com/Microsoft/hdfs-mount.git && cd hdfs-mount && make && \
    cp hdfs-mount /bin && cd .. && rm -rf hdfs-mount

ENV PATH=/usr/local/nvidia/bin:/usr/local/cuda/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/root/.local/bin:/usr/bin:/bin:/sbin

WORKDIR /root
