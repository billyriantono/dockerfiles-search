FROM ubuntu:bionic

# Install dependencies
RUN apt update && apt install -y --no-install-recommends \
    gnupg2 \
    ca-certificates \
    wget \
    openjdk-8-jre-headless \
    mercurial \
    make \
 && rm -rf /var/lib/apt/lists/*

# Get gcc-arm-embedded key
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B4D03348F75E3362B1E1C2A1D1FAA6ECF64D33B0

# Add ggc-arm-embedded ppa
RUN echo "deb http://ppa.launchpad.net/team-gcc-arm-embedded/ppa/ubuntu bionic main" > /etc/apt/sources.list.d/team-gcc-arm-embedded-ubuntu-ppa-bionic.list

# Install gcc-arm-armbedded
RUN apt update && apt install -y --no-install-recommends \
    gcc-arm-embedded \
 && rm -rf /var/lib/apt/lists/*

# Download and extract GNU MCU Eclipse
RUN wget -qO- https://api.github.com/repos/gnu-mcu-eclipse/org.eclipse.epp.packages/releases/latest | sed -n 's/.*browser_download_url.*\(https.*linux.*x86_64.*tar.gz\)"/\1/p' | wget -qi - \
 && tar -xzf *.tar.gz \
 && rm *.tar.gz \
 && mv eclipse /opt/eclipse

# Add Eclipse to PATH
RUN echo 'PATH="$PATH:/opt/eclipse"' >> /root/.profile

# Add Eclipse MCU build script
ADD eclipse-mcu-build-all /usr/bin
