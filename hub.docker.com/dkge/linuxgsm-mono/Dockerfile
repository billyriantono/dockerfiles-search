#
# LinuxGSM Dockerfile
#
# https://github.com/MrDKGE/LinuxGSM-Docker-Mono5
#

FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

## Add the Mono repository
RUN apt update -y && \
	apt install -y \
		ca-certificates \
		gnupg 
		
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
	echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list && \
	apt update -y

## Base System
RUN dpkg --add-architecture i386 && \
	apt update -y && \
	apt install -y \
		mailutils \
		postfix \
		curl \
		wget \
		file \
		bzip2 \
		gzip \
		unzip \
		bsdmainutils \
		python \
		util-linux \
		binutils \
		bc \
		jq \
		tmux \
		lib32gcc1 \
		libstdc++6 \
		libstdc++6:i386 \
		apt-transport-https \
		mono-complete

## lgsm.sh
RUN wget https://linuxgsm.com/dl/linuxgsm.sh

## user config
RUN groupadd -g 750 -o lgsm && \
	adduser --uid 750 --disabled-password --gecos "" --ingroup lgsm lgsm && \
	chown lgsm:lgsm /linuxgsm.sh && \
	chmod +x /linuxgsm.sh && \
	cp /linuxgsm.sh /home/lgsm/linuxgsm.sh && \
	usermod -G tty lgsm && \
	chown -R lgsm:lgsm /home/lgsm/ && \
	chmod 755 /home/lgsm

USER lgsm
WORKDIR /home/lgsm
VOLUME [ "/home/lgsm" ]

# need use xterm for LinuxGSM
ENV TERM=xterm

## Docker Details
ENV PATH=$PATH:/home/lgsm

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["bash","/entrypoint.sh" ]
