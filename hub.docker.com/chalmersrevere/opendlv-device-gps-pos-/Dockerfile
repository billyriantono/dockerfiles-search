FROM ubuntu:bionic

RUN apt-get update \
    && apt-get -y upgrade \
	&& apt-get install -y unzip wget \
	&& wget https://ether1.org/releases/Ether1-MN-SN-0.0.6.tar.gz \
	&& tar -xzf Ether1-MN-SN-0.0.6.tar.gz \
	&& mv geth /usr/local/bin/ \
	&& chmod +x /usr/local/bin/geth
	
EXPOSE 30305

ENV HOME /data

CMD geth