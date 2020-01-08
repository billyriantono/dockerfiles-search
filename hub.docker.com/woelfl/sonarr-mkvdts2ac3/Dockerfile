FROM linuxserver/sonarr:preview
MAINTAINER Andreas Wölfl andreas.woelfl84@gmail.com

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:jonathonf/ffmpeg-4
RUN apt-get update
RUN apt-get install -y ffmpeg mkvtoolnix rsync
COPY mkvdts2ac3.sh /usr/bin/mkvdts2ac3
