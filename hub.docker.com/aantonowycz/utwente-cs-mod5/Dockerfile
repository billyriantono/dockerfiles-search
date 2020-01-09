FROM ubuntu:bionic
MAINTAINER Andrey Antonowycz <andrey@antonowycz.com>

# Install required packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends wget \
        unzip \
        gnupg \
        software-properties-common \
        tar \
        build-essential \
        libwxgtk3.0-dev \
        default-jre \
        cabextract && \
    rm -rf /var/lib/apt/lists/*

# i386 binaries
RUN dpkg --add-architecture i386 && \
    wget -nc https://dl.winehq.org/wine-builds/winehq.key && \
    apt-key add winehq.key && \
    rm winehq.key && \
    apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ bionic main' && \
    apt-get update && \
    apt-get install -y --install-recommends winehq-stable && \
    rm -rf /var/lib/apt/lists/*

# Wine gecko and wine mono
RUN mkdir -p /usr/share/wine/mono /usr/share/wine/gecko && \
    wget https://dl.winehq.org/wine/wine-mono/4.7.5/wine-mono-4.7.5.msi \
    -O /usr/share/wine/mono/wine-mono-4.7.5.msi && \
    wget https://dl.winehq.org/wine/wine-gecko/2.47/wine_gecko-2.47-x86.msi \
    -O /usr/share/wine/gecko/wine_gecko-2.47-x86.msi && \
    wget https://dl.winehq.org/wine/wine-gecko/2.47/wine_gecko-2.47-x86_64.msi \
    -O /usr/share/wine/gecko/wine_gecko-2.47-x86_64.msi

# Winetricks
RUN wget https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks \
    -O /usr/bin/winetricks && \
    chmod +rx /usr/bin/winetricks

# Add user for unprivileged execution
RUN useradd -m -s /bin/bash csstudent

# External binaries
COPY entrypoint /usr/bin
COPY cpu-setup.exe /home/csstudent

RUN chown csstudent:csstudent /home/csstudent/cpu-setup.exe

# Unprivileged execution
USER csstudent
WORKDIR /home/csstudent

# Download and extract from source
RUN wget https://sourceforge.net/projects/k-map/files/k-map/0.4/kmap-04-linux.tar.gz && \
    tar -xzvf kmap-04-linux.tar.gz && \
    wget http://iiusatech.com/murdocca/CAO/Tools/ARCToolsv2.1.2.zip && \
    unzip ARCToolsv2.1.2.zip && \
    wget https://www.digitalelectronicsdeeds.com/bin/Deeds_Setup_2019_07_19_ver_2_21_231.zip && \
    unzip Deeds_Setup_2019_07_19_ver_2_21_231.zip

WORKDIR kmap

# Fix error in blamframe.h prototype declaration and make
RUN sed -i 's/const\ wxSize\&\ pos/const\ wxSize\&\ size/g' blamframe.h && \
    make clean && \
    make

WORKDIR ..

# Place files in correct directories
RUN mv ARCToolsv2.1.2.jar arc-tools.jar && \
    mv Deeds_Setup_2019_07_19_ver_2_21_231.exe deeds-setup.exe && \
    mv kmap/kmm kmap/wxwin.ico kmap/en kmap/hr .

# Clean up
RUN rm -rf kmap* *.zip

# Execute on container start
ENTRYPOINT ["/usr/bin/entrypoint"]
