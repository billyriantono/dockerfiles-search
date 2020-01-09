FROM ubuntu:16.04

RUN apt-get update \
    && apt-get install -y software-properties-common curl \
    && add-apt-repository ppa:jonathonf/python-3.6 \
    && apt-get remove -y software-properties-common \
    && apt autoremove -y \
    && apt-get update \
    && apt-get install -y build-essential \
    && apt-get install -y net-tools \
    && apt-get install -y openssh-server \
    && apt-get install -y telnet \
    && apt-get install -y git \
    && apt-get install -y mercurial \
    && apt-get install -y vim \
    && apt-get install -y qemu-system-arm \
    && apt-get install -y qemu-system-x86 \
    && apt-get install -y python3.6 \
    && curl -o /tmp/get-pip.py "https://bootstrap.pypa.io/get-pip.py" \
    && python3.6 /tmp/get-pip.py \
    && apt-get remove -y curl \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /
RUN git clone https://github.com/Rahix/tbot.git \
    && cd /tbot \
    && python3.6 setup.py install --user

RUN mkdir -p /root/.ssh
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN echo 'root:root' | chpasswd

COPY bashrc /root/.bashrc
COPY init /init

ENTRYPOINT ["/init"]
CMD ["bash"]
