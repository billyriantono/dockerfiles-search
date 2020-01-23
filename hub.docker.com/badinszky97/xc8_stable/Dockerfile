FROM ubuntu:latest

# Install dependencies
RUN dpkg --add-architecture i386 \
 && apt update \
 && apt install -y --no-install-recommends curl libc6:i386 \
        libx11-6:i386 libxext6:i386 libstdc++6:i386 libexpat1:i386 \
        libxext6 libxrender1 libxtst6 libgtk2.0-0 make \
 && rm -rf /var/lib/apt/lists/*

# Install python modules
RUN apt update \
 && apt install -y python-pip python-setuptools \
 && rm -rf /var/lib/apt/lists/* \
 && pip install --upgrade pip
RUN pip install glob2
RUN apt autoclean && apt autoremove


# Download and install XC8 compiler
RUN curl -fSL -A "Mozilla/4.0" -o /tmp/xc8.run "http://ww1.microchip.com/downloads/en/DeviceDoc/xc8-v2.05-full-install-linux-installer.run" \
 && chmod a+x /tmp/xc8.run \
 && /tmp/xc8.run --mode unattended --netservername localhost --LicenseType FreeMode \
 && rm /tmp/xc8.run
ENV PATH $PATH:/opt/microchip/xc8/v2.05/bin

# Download and install MPLAB X IDE
# Use url: http://www.microchip.com/mplabx-ide-linux-installer to get the latest version

RUN curl -fSL -A "Mozilla/4.0" -o /tmp/mplabx-installer.tar "http://ww1.microchip.com/downloads/en/DeviceDoc/MPLABX-v3.40-linux-installer.tar" \
 && tar xf /tmp/mplabx-installer.tar && rm /tmp/mplabx-installer.tar \
 && USER=root ./*-installer.sh --nox11 \
    -- --unattendedmodeui none --mode unattended && rm /MPLABX-v3.40-linux-installer.sh

ENV PATH $PATH:/opt/microchip/mplabx/v3.40/bin

