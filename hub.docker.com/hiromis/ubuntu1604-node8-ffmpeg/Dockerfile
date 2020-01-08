FROM hiromis/ubuntu1604-node8
MAINTAINER hiromis

# install ffmpeg
RUN apt -y install software-properties-common python-software-properties
RUN add-apt-repository -y ppa:jonathonf/ffmpeg-3 
RUN apt update
RUN apt -y install ffmpeg libav-tools x264 x265

