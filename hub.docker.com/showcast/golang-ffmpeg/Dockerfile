FROM golang:1.6.3

MAINTAINER Anton Martsen <martsen.anton@gmail.com>

RUN apt-get update && apt-get -y upgrade

# add with ffmpeg - https://www.assetbank.co.uk/support/documentation/install/ffmpeg-debian-squeeze/ffmpeg-debian-jessie/
RUN echo deb http://www.deb-multimedia.org jessie main non-free >>/etc/apt/sources.list && echo deb-src http://www.deb-multimedia.org jessie main non-free >>/etc/apt/sources.list
RUN apt-get update && apt-get install -y --force-yes deb-multimedia-keyring && apt-get update && apt-get install -y ffmpeg