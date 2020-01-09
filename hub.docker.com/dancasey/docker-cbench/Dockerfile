FROM ubuntu:14.04
MAINTAINER Dan Casey <dc181@icloud.com>

RUN apt-get update && apt-get install -y --no-install-recommends \
    autoconf \
    automake \
    ca-certificates \
    curl \
    git \
    iproute2 \
    iputils-ping \
    libtool \
    net-tools \
    openssh-server \
    sudo \
    tcpdump

RUN git clone git://github.com/mininet/mininet \
    && cd mininet \
    && git checkout -b 2.2.1 2.2.1 \
    && cd ..

RUN mininet/util/install.sh -n
RUN apt-get install -y --no-install-recommends patchutils
RUN mininet/util/install.sh -f
RUN mininet/util/install.sh -b

# Using ENTRYPOINT so that container can be run with arguments to override CMD, e.g.,
#   docker run -it --rm --link ryu dancasey/cbench -c ryu -p 6653 -s 2
ENTRYPOINT ["cbench"]
CMD ["-c", "controller", "-p", "6653"]
