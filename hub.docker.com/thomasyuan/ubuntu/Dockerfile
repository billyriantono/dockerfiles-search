FROM ubuntu:16.04

# Install essential packages for development
RUN apt-get update && apt-get install -y \
    gawk \
    wget \
    git-core \
    diffstat \
    unzip \
    texinfo \
    gcc-multilib \
    build-essential \
    curl \
    python3 \
    locales \
    iputils-ping \
    net-tools \
    vim \
    xterm \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# set locale and lang
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen

# create non-root user
RUN groupadd -g 999 thomas && \
    useradd -r -u 999 -g thomas -m thomas && \
    usermod -aG sudo thomas && \
    echo "thomas ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
# switch user
USER thomas

WORKDIR /home/thomas

COPY . .
RUN  ./init.sh && rm init.sh

