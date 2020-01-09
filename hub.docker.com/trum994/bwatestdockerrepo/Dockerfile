FROM ubuntu:14.04

MAINTAINER akurdoglu@ashion.com

RUN apt-get update && apt-get install -y \
	wget \
	vim \
	git

RUN mkdir -p /home/ashion/bin

ENV PATH=$PATH:/home/ashion/bin
ENV HOME=/home/ashion

#get bwa
ENV PACKAGE=bwakit-0.7.12_x64-linux.tar.bz2
ENV URL=https://sourceforge.net/projects/bio-bwa/files/bwakit/bwakit-0.7.12_x64-linux.tar.bz2/download
ENV DEST=/home/ashion/bin

RUN wget $URL -O $DEST/$PACKAGE
RUN tar -xvf $DEST/$PACKAGE -C $DEST
RUN rm $DEST/$PACKAGE

COPY runBWA.sh $DEST

ENTRYPOINT ["/home/ashion/bin/runBWA.sh"]
