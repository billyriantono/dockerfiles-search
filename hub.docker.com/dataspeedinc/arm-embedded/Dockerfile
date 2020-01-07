FROM ubuntu:bionic

# AWS APT mirrors
RUN sed -i 's+http://security.ubuntu.com/+http://archive.ubuntu.com/+g' /etc/apt/sources.list \
 && sed -i 's+http://archive.ubuntu.com/+http://us-east-1.ec2.archive.ubuntu.com/+g' /etc/apt/sources.list \
 && apt update \
 && rm -rf /var/lib/apt/lists/*

# Install git and ssh
RUN apt update \
 && apt install -y git ssh-client \
 && rm -rf /var/lib/apt/lists/*

# Install dependencies
RUN apt update \
 && apt install -y --no-install-recommends \
    gnupg2 \
    make \
    cmake \
 && rm -rf /var/lib/apt/lists/*

# Get key, add ppa and install gcc-arm-embedded
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B4D03348F75E3362B1E1C2A1D1FAA6ECF64D33B0 \
 && echo "deb http://ppa.launchpad.net/team-gcc-arm-embedded/ppa/ubuntu bionic main" > /etc/apt/sources.list.d/team-gcc-arm-embedded-ubuntu-ppa-bionic.list \
 && apt update && apt install -y --no-install-recommends gcc-arm-embedded \
 && rm -rf /var/lib/apt/lists/*

# Add Arm embedded build script
ADD arm-embedded-build-all /usr/bin
