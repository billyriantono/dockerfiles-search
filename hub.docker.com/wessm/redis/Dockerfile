FROM ubuntu:16.04

LABEL maintainer="Michael Wess <michael.wess@boku.ac.at>"

USER root

RUN apt-get update -y && \
	apt-get upgrade -y && \
	apt-get install -y --no-install-recommends \
		gcc \
		wget \
		sudo \
		make \
		build-essential \
		python-pip  && \
		#postgis \
		#gdal-bin \
		#libgdal-dev \
		#libgeos-dev \
		#python-dev \
		#libpython-dev \
		#libproj-dev \
		#python-gdal \
		#imagemagick && \
	apt-get clean autoclean && \
	apt-get autoremove -y && \
	rm -rf /var/lib/apt/lists/*


RUN useradd --password 'password' \
	--uid 1000 \
	--create-home \
	--no-log-init \
	--shell /bin/bash \
	redis

RUN adduser redis sudo
#	mkdir /home/user/scripts

USER redis

WORKDIR /home/redis

RUN cd ~ && \
	wget http://download.redis.io/redis-stable.tar.gz && \
	tar xvzf redis-stable.tar.gz && \
	cd redis-stable && \
	make

USER root

RUN cd /home/redis/redis-stable && \
	make install && \
	cd .. && \
	rm -rf redis-stable

RUN pip install setuptools wheel && \
	apt-get update -y && \
	apt-get install -y --no-install-recommends \
		dpkg-dev \
		g++ \
		libc6-dev \
		make \
		python3-dev \
		python3-pip \
		libgcc1 \
		libxml2-dev \
		zlib1g-dev && \
	pip install \
	redis \
	huey
	#psycopg2-binary \
	#imutils \
	#shapely \
	#rasterstats \
	#fiona \
	#pygeoj \
	#gdal \
	#geopandas \
	#pyshp \
	#sentinelhub \
	#sentinelsat


USER redis


#ADD *.py /home/user/scripts/
#ADD *.cfg /home/user/scripts/

#RUN mkdir /home/mischa/s2overview

#CMD ["redis-server","--daemonize","yes"]
ENTRYPOINT /usr/local/bin/redis-server --protected-mode no
#--daemonize yes
#&& /usr/local/bin/huey_consumer.py scripts/download_overview_for_tile.huey -k process -w 4 --logfile=/home/user/huey.log
#ENTRYPOINT /bin/bash


