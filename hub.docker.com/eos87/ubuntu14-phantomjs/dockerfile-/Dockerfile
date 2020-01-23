FROM httpd:latest

RUN apt-get update && apt-get install -y python python-dev python-pip \
   libxft-dev libfreetype6 libfreetype6-dev libsm6 libxext6

RUN pip install --upgrade pip
RUN pip install matplotlib
RUN pip install opencv-python
RUN pip install numpy
RUN pip install scipy
RUN pip install Pillow