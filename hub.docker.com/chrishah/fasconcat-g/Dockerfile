FROM ubuntu:16.04

MAINTAINER <christoph.hahn@uni-graz.at>

RUN apt-get update && apt-get -y upgrade && \
        apt-get install -y build-essential vim git 

WORKDIR /usr/src

RUN git clone --recursive https://github.com/PatrickKueck/FASconCAT-G.git && \
	cd FASconCAT-G && \
	git reset --soft ccbc89aa7c811dc22a42805d77222cc69b3c7439 && \
	perl -pi -e 'tr[\r][]d' FASconCAT-G_v1.04.pl && \
	chmod a+x FASconCAT-G_v1.04.pl && \
	ln -s $(pwd)/FASconCAT-G_v1.04.pl /usr/bin/FASconCAT-G.pl

#create working directory and move to entrypoint
VOLUME /home/data
WORKDIR /home/data

