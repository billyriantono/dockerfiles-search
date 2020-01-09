# https://github.com/bbinet/docker-mplabx/blob/master/Dockerfile
# http://microchip.wikidot.com/install:mplabx-lin64
FROM debian:stretch-slim
LABEL maintainer="nathan@magothyrivertech.com"

# http://microchip.wikidot.com/install:mplabx-lin64#toc3
RUN dpkg --add-architecture i386 \
    && apt-get update -yq \
    && apt-get install -yq --no-install-recommends \
    libc6:i386 libx11-6:i386 libxext6:i386 libstdc++6:i386 libexpat1:i386 \
    curl ca-certificates git procps make \
    && apt-get purge && apt-get clean

# Download and install XC8 compiler
RUN curl -fSL -o xc8.run "http://ww1.microchip.com/downloads/en/DeviceDoc/xc8-v2.00-full-install-linux-installer.run" \
    && chmod a+x xc8.run \
    && ./xc8.run --mode unattended --netservername localhost \
    && rm xc8.run
ENV PATH /opt/microchip/xc8/v2.00/bin:$PATH

# Download and install MPLAB X IDE
RUN curl -fSL -o mplabx-installer.tar "http://ww1.microchip.com/downloads/en/DeviceDoc/MPLABX-v5.10-linux-installer.tar" \
    && tar xf mplabx-installer.tar && rm mplabx-installer.tar \
    && USER=root ./MPLABX-v5.10-linux-installer.sh --nox11 -- --mode unattended --ipe 0 \
    && rm ./MPLABX-v5.10-linux-installer.sh
ENV PATH /opt/microchip/mplabx/v5.10/mplab_ide/bin:$PATH
