FROM ubuntu:18.04


ENV DEBIAN_FRONTEND noninteractive

RUN set -x && \
	apt-get update -y && \
    DEBIAN_FRONTEND=noninteractive  apt-get install --no-install-recommends --no-install-suggests -y language-pack-en \
    tzdata \
    net-tools \
    htop \
    vim \
    unzip \
    mc \
    gcc \
    gnupg1 \
    gnupg \
    apt-transport-https \
    ca-certificates \
    autoconf \
    dpkg-dev \
    file \
    g++ \
    libc-dev \
    make \
    pkg-config \
    re2c \
    dirmngr \
    curl \
    xz-utils \
    openssl \
    perl \
    git \
    tcpdump \
    telnet \
    iputils-ping \
    wget \
    bzip2 \
    apt-utils \
    debconf \
    software-properties-common \
    build-essential \
    cmake \
    cron

RUN set -x && \
    update-alternatives --set editor /usr/bin/vim.basic && \
    update-locale LANG=en_US.UTF-8 && \
    rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/UTC /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean && \
    rm -r /var/lib/apt/lists/*

COPY lockrun.c /tmp
RUN set -x && \
    gcc /tmp/lockrun.c -o lockrun && \
    mv lockrun /usr/local/bin/

# overwrite this with 'CMD []' in a dependent Dockerfile
CMD ["/bin/bash"]