FROM jjanzic/docker-python3-opencv:opencv-4.0.1
MAINTAINER aakhter

COPY requirements.txt /tmp/requirements.txt
#COPY veehive-tools/ /tmp/veehive-tools/
RUN pip install --upgrade pip
RUN pip install -r /tmp/requirements.txt 
RUN apt-get update
RUN apt-get install -y ffmpeg
RUN wget https://sourceforge.net/projects/libjpeg-turbo/files/2.0.2/libjpeg-turbo-official_2.0.2_amd64.deb/download# \
	-O libjpeg-turbo-official_2.0.2_amd64.deb
RUN dpkg -i libjpeg-turbo-official_2.0.2_amd64.deb


