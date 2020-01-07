#image updated with debian and vnc
FROM miguelwill/debian-vnc:firefox

LABEL maintainer "miguelwill@gmail.com"

# Use the latest version of winetricks
RUN curl -SL 'https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks' -o /usr/local/bin/winetricks \
        && chmod +x /usr/local/bin/winetricks

RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    wget \
    unrar-free unzip cabextract \
    wine && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

VOLUME /c

