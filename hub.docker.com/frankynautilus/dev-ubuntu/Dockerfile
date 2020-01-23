ARG UBUNTU_VERSION=18.04
FROM ubuntu:${UBUNTU_VERSION}

# build-essential depends (dpkg-dev g++ gcc libc6-dev make)
# cgo depends (gcc)
RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils \
    # c++
    build-essential \
    gdb \
    cmake \
    # tools
    vim \
    curl \
    wget \
    tcpdump \
    # pcap
    libcap-dev \
    pkg-config \
    # ZeroMQ
    libzmq3-dev \
    # go
    golang-go \
    # ssh
    openssh-server \
    && mkdir -p /var/run/sshd /root/.ssh \
    && echo 'root:root' | chpasswd \
    && sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config \
    # clean
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # volume
    && mkdir -p /go /project

# env for go
ENV GOPATH /go
ENV PATH $GOPATH/bin:$PATH

VOLUME ["/go", "/project"]

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]