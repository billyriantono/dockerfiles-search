FROM maciver40/ubuntu-base
LABEL maintainer="robert@eisenmann.email"

VOLUME [ "/download" ]
VOLUME [ "/config" ]

ADD https://github.com/squell/id3/releases/download/0.80/id3mtag_0.80-1_amd64.deb /opt/id3mtag.deb

EXPOSE 5000

RUN \
    apt-get update && \
    apt-get install -y \
           ffmpeg \
           python \
           python3 \
           python3-tornado \
           streamripper \
           xsltproc && \
    mkdir /scriptsrv && cd /scriptsrv && \
    wget https://github.com/bugy/script-server/releases/download/dev/script-server.zip && \
    curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl && \
    unzip script-server.zip && \
    apt install -y /opt/id3mtag.deb
