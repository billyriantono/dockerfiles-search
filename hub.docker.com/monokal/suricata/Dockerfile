FROM ubuntu:latest

# APT packages to install.
ENV APT_PACKAGES \
    wget \
    git \
    cmake \
    python-pip \
    libpcre3 \
    libpcre3-dbg \
    libpcre3-dev \
    build-essential \
    autoconf \
    automake \
    libtool \
    libpcap-dev \
    libnet1-dev \
    libyaml-0-2 \
    libyaml-dev \
    zlib1g \
    zlib1g-dev \
    libcap-ng-dev \
    libcap-ng0 \
    make \
    libmagic-dev \
    libjansson-dev \
    libjansson4 \
    pkg-config \
    libnetfilter-queue-dev \
    libnetfilter-queue1 \
    libnfnetlink-dev \
    libnfnetlink0 \
    libhyperscan4 \
    ragel \
    liblua5.1-dev

# PIP packages to install.
ENV PIP_PACKAGES \
    pip \
    pyyaml \
    suricata-update

# Tell systemd we're in Docker.
ENV container docker

# Install the APT packages.
RUN apt-get -y update && \
    apt-get -y install ${APT_PACKAGES}

# Copy in the Suricata source and enter the directory.
COPY . /tmp/suricata
WORKDIR /tmp/suricata

# Drop in the LibHTP parser.
RUN git clone https://github.com/OISF/libhtp

# Compile and install Suricata from source.
# TODO: "make install-conf" doesn't add suricata to PATH,
# so we're using "install-full" for now.
RUN chmod +x autogen.sh && ./autogen.sh && \
    ./configure --enable-geopip --enable-lua --enable-nfqueue --prefix=/usr --sysconfdir=/etc --localstatedir=/var && \
    make && \
    make install-full && \
    ldconfig

# Install the PIP packages.
RUN pip install --pre --upgrade ${PIP_PACKAGES}

# Cleanup.
WORKDIR /
RUN rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*

# Inject an entrypoint script to run suricata-update then suricata
# with suricata-update's rules applied.
RUN echo "#!/bin/sh\nsuricata-update && suricata -S /var/lib/suricata/rules/suricata.rules \$@" > /usr/local/bin/entrypoint.sh && \
    chmod +x /usr/local/bin/entrypoint.sh

# Additional arguments are provided at the run command and passed
# directly to Suricata by the entrypoint script.
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
