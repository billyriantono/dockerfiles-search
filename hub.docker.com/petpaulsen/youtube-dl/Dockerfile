FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
	ffmpeg \
	python3 \
	python3-pip
RUN pip3 install --upgrade pip
RUN pip3 install --upgrade youtube-dl
WORKDIR ~
ENTRYPOINT ["youtube-dl"]
