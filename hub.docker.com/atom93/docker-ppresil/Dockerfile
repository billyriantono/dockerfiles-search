FROM ubuntu:16.04

SHELL ["/bin/bash", "-c"]

RUN apt-get update && \
	apt-get install -y python3 && \
	apt-get install -y python3-pip && \
	python3 -m pip install --upgrade pip && \
	apt-get install -y software-properties-common && \
	add-apt-repository -y ppa:ubuntugis/ubuntugis-unstable && \
	apt-get update && \
	apt-get install -y gdal-bin=2.2.2+dfsg-1~xenial1 python3-gdal=2.2.2+dfsg-1~xenial1 &&\
	pip3 install pandas && \
	pip3 install scipy && \
	pip3 install -U statsmodels && \
	pip3 install spectral && \
	mkdir ./Tmp && \
	touch ./Tmp/MSaviFeat && \
	chmod 777 ./Tmp/MSaviFeat && \
	apt-get install -y zip && \
	apt-get install -y unzip && \
	echo -e "0\n0\n0\n0" >> /BBfile.txt