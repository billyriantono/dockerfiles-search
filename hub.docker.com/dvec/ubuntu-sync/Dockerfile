FROM ubuntu:latest

## Base System
RUN dpkg --add-architecture i386 && \
	apt update -y && \
	apt install -y \
    		sudo \
    		vim \
		curl \
		wget \
		gzip \
		unzip \
		python3.7 \
		python3-pip \
		ffmpeg \
		telnet \
		apt-transport-https \
		&& apt-get clean \
	  && rm -rf /var/lib/apt/lists/*
	  
RUN wget -q -O - https://mkvtoolnix.download/gpg-pub-moritzbunkus.txt | sudo apt-key add - && \
	apt update -y && \
	apt install -y \
	mkvtoolnix

RUN pip3 install click pillow ffmpeg-python
    
RUN export LC_ALL=C.UTF-8

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["bash","/entrypoint.sh"]
