FROM debian:buster
MAINTAINER janpfo

RUN apt update
RUN	apt install -y pkg-config python3-pip python3-pybind11 libsphinxbase3 libsphinxbase-dev pocketsphinx ffmpeg python3-venv pkg-config libpocketsphinx-dev libavformat-dev libswresample-dev libavdevice-dev libavfilter-dev python3-pocketsphinx git
RUN	apt clean
RUN	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
	
WORKDIR /app

RUN	git clone --single-branch --branch development https://github.com/morpheus65535/bazarr.git 
RUN	pip3 install --no-cache-dir -U  -r \
	/app/bazarr/requirements.txt
	
RUN	git clone -b '0.13' https://github.com/sc0ty/subsync.git

WORKDIR /app/subsync

RUN	cp subsync/config.py.template subsync/config.py 
RUN sed -i '/wxPython>=4.0/d' ./requirements.txt
RUN	pip3 install -r requirements.txt 

WORKDIR /app/subsync/gizmo

RUN python3 setup.py build
RUN python3 setup.py install

WORKDIR /app/subsync

RUN python3 setup.py build
RUN python3 setup.py install

WORKDIR /
	
# add local files
# COPY root/ /

# ports and volumes
EXPOSE 6767
VOLUME /config /data
