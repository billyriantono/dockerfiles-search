FROM	python:3.8-slim

RUN	apt-get update && apt-get -y --no-install-recommends install wget

RUN	wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl && \
	chmod a+rx /usr/local/bin/youtube-dl

