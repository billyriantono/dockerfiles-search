FROM debian:buster-slim
LABEL maintainer "Nikhil Dhandre <nik.digitronik@live.com>"

# Install wine and winetricks

RUN apt-get update && apt-get install -y \
	wine wget\
	--no-install-recommends && \
	dpkg --add-architecture i386 && \
	apt-get update && \
	apt-get install -y \
	wine32 ca-certificates cabextract \
	--no-install-recommends && \
	wget -O /usr/bin/winetricks https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks && \
        chmod +x /usr/bin/winetricks && \
	rm -rf /var/lib/apt/lists/*

ENV HOME /root
WORKDIR $HOME
