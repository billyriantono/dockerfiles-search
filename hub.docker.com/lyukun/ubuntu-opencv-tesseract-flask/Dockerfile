FROM ubuntu:18.04
LABEL  maintainer="LK"

RUN \
#==================================================
# Python3.6
#==================================================
  echo 'deb http://security.ubuntu.com/ubuntu xenial-security main' >> /etc/apt/sources.list && \
  apt-get update &&\
  #apt-get -qqy upgrade &&\
  apt-get -qqy --no-install-recommends install \
    python3.6 \
    python3-pip \
    python3-setuptools \
    curl \
    tesseract-ocr \
    libjpeg-dev libtiff5-dev libjasper1 libjasper-dev libpng-dev \
    libgtk2.0-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libatlas-base-dev gfortran &&\
    #python-imaging &&\
#==================================================
# Flask
#==================================================
  pip3 install wheel &&\
  pip3 install flask_restplus &&\
  pip3 install requests &&\
  pip3 install paramiko &&\
  pip3 install opencv_python &&\
  pip3 install pytesseract &&\
  pip3 install vncdotool &&\

#==================================================
# apt clean
#==================================================
  apt-get clean && rm -rf /var/lib/apt/lists/*

#COPY eng.traineddata /usr/share/tesseract-ocr/4.00/tessdata/eng.traineddata
#COPY script /script
#CMD ["python3", "/script/main.py"]
