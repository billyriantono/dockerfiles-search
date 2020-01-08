FROM node:latest

MAINTAINER Juanjo Mata <juanjo.mata@gmail.com>

ENV OPENCV_VERSION 3.1.0

COPY build.sh /build.sh
RUN bash /build.sh \
	&& rm /build.sh

ENV LD_LIBRARY_PATH /usr/local/lib

RUN apt-get -y install golang cmake

RUN cd /opt && git clone https://github.com/VISIONAI/VMXwebcam.git && cd VMXwebcam && ./linux_builder.sh

CMD ["node"]
