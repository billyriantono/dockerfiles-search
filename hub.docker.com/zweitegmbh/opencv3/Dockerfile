#Dockerfile for rustiberry-vision

# Pull base image.
FROM jrottenberg/ffmpeg

MAINTAINER lino <lino@zweite.gmbh>

ADD install.sh /
ADD install_opencv.sh /

# Define working directory.
WORKDIR /

RUN /install.sh
ENTRYPOINT []
