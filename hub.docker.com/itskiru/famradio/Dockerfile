FROM ubuntu:zesty

RUN apt update
RUN apt upgrade -y
RUN apt install -y curl
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash
RUN apt update
RUN apt install -y build-essential ffmpeg git python nodejs
RUN apt install -y libcairo2-dev libjpeg8-dev libpango1.0-dev libgif-dev g++
RUN apt autoremove -y

RUN mkdir -p /usr/src/2DFAMRADIO
WORKDIR /usr/src/2DFAMRADIO

COPY . .

RUN npm install

ENV TOKEN= \
	COMMAND_PREFIX= \
	OWNERS= \
	DB= \
	REDIS= \
	STREAM= \
	RADIO_CHANNELS= \
	GOOGLE_API= \
	SOUNDCLOUD_API= \
	DEFAULT_VOLUME= \
	MAX_LENGTH= \
	MAX_SONGS= \
	PASSES=

CMD node sharder.js
