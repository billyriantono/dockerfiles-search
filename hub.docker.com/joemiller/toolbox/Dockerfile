FROM gcr.io/google-containers/toolbox:20180309-00
# https://console.cloud.google.com/gcr/images/google-containers/GLOBAL/toolbox?gcrImageListsize=50

RUN sed -i 's/$/ contrib non-free/' /etc/apt/sources.list && rm -rf /var/lib/apt/lists/* && apt-get update

# RUN apt-get update -q \
#     && apt-get install -qy \
#       strace \
#       tcpdump \
#       perf \
#       htop \
#       dstat \
#       atop \
#       sar \
#       iostat \
#       blktrace \
#       iozone \
#       vmstat \
#       slabtop \
#       pidstat \
#       lsof \
#       iperf \
#       iftop \
#     && apt-get -y autoremove \
#     && apt-get -y clean \
#     && rm -rf /var/lib/apt/lists/* \
#     && rm -rf /tmp/*


# Convenience
RUN apt-get install -y --no-install-recommends \
        file     \
        git      \
        less     \
        man-db   \
        manpages \
        vim      \
        zsh

# Generic
RUN apt-get install -y --no-install-recommends \
        atop    \
        dstat   \
        htop    \
        ltrace  \
        strace  \
        sysstat

# IO
RUN apt-get install -y --no-install-recommends \
        blktrace \
        iotop    \
        iozone3  \
        lsof

# Networking
RUN apt-get install -y --no-install-recommends \
        arping          \
        bridge-utils    \
        ca-certificates \
        curl            \
        ethtool         \
        iftop           \
        iperf           \
        iproute2        \
        mtr-tiny        \
        net-tools       \
        nicstat         \
        nmap            \
        tcpdump

# perf
RUN apt-get install -y --no-install-recommends \
        linux-tools     \
        perf-tools-unstable

# Golang
ENV GOLANG_VERSION 1.10.3
ENV GOPATH /go
RUN curl -L https://golang.org/dl/go${GOLANG_VERSION}.linux-amd64.tar.gz \
        | tar -C /usr/local -xzf -
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

# https://github.com/google/embiggen-disk
RUN go get github.com/google/embiggen-disk

# Sysdig
# RUN curl -s https://s3.amazonaws.com/download.draios.com/DRAIOS-GPG-KEY.public \
#         | apt-key add - \
#     && curl -s http://download.draios.com/stable/deb/draios.list \
#         > /etc/apt/sources.list.d/draios.list \
#     && curl -s http://download.draios.com/apt-draios-priority \
#         > /etc/apt/preferences.d/apt-draios-priority \
#     && apt-get update \
#     && apt-get install -y --no-install-recommends \
#         gcc     \
#         gcc-4.8 \
#         sysdig  \
#     && ln -s /media/root/lib/modules /lib/modules

# Docker
# RUN echo "deb https://get.docker.com/ubuntu docker main" \
#         > /etc/apt/sources.list.d/docker.list \
#     && apt-key adv --keyserver hkp://pgp.mit.edu \
#         --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9 \
#     && apt-get install -y --no-install-recommends apt-transport-https \
#     && apt-get update \
#     && apt-get install -y --no-install-recommends lxc-docker-1.6.2

CMD ["/bin/zsh"]
