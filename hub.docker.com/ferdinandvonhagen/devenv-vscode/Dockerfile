# Remote Visual Studio Instance
FROM ubuntu:16.04

WORKDIR /home

# libasound2:i386 
RUN dpkg --add-architecture i386 && \
    apt-get update && \
    apt-get install -y wget libgtk2.0-0:i386 libxtst6:i386 libgconf-2-4:i386 libasound2 libxss1 python-pip && \ 
    wget --quiet -O vscode-amd64.deb https://go.microsoft.com/fwlink/?LinkID=760868 && \
    dpkg -i vscode-amd64.deb; apt-get install -f -y && \
    rm vscode-amd64.deb && \
    rm -rf /var/lib/apt/lists/* && \
    sed -i 's/BIG-REQUESTS/_IG-REQUESTS/' /usr/lib/x86_64-linux-gnu/libxcb.so.1

RUN groupadd -r developer -g 1000 && \
    useradd -u 1000 -r -g developer -d /developer -s /bin/bash -c "Software Developer" developer && \
    mkdir /developer && \
    mkdir /developer/.vscode && \
    mkdir /developer/.config && \
    mkdir /developer/.config/Code && \
    chown -R developer:developer /developer

USER developer

ENV DISPLAY 192.168.1.8:0

# mount points
VOLUME ["/developer"]

CMD ["code", "--verbose", "--disable-gpu"]