FROM centos:7

RUN yum -y install \
    bind-utils \
    openssh-clients \
    iperf3 \
    iproute \
    nc \
    wget \
    vim \
    tcpdump \
    man \
    net-tools \
    epel-release && \
    yum -y install python-pip && \
    yum clean all

ENTRYPOINT ["/bin/nc", "-vlkp", "7000"]
EXPOSE 7000
