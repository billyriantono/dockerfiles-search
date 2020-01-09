FROM ubuntu:16.04
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y wget zip
WORKDIR /home/piper/piper-builder/piper2
VOLUME /mnt/scratch
ENV PIPERCODE_DOWNLOAD v2.4.2.img.zip
RUN wget http://piper-sdcard-images.s3-website-us-west-1.amazonaws.com/release/$PIPERCODE_DOWNLOAD
RUN unzip $PIPERCODE_DOWNLOAD -d /mnt/scratch
CMD ls
