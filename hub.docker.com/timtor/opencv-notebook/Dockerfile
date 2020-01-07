FROM python:3.7

WORKDIR /code

# update in quiet mode: no output except error
RUN apt-get -qq update 

# Install opencv 
RUN apt-get -qq install -y \
    # developer tools
    wget git \
    build-essential cmake unzip pkg-config\
    # image/ video libraries
    libjpeg-dev libpng-dev libtiff-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libxvidcore-dev libx264-dev \
    # use prebuild opencv 4.0.0
&&  pip install opencv-python

CMD [ "bash" ]
