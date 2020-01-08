FROM ubuntu:16.04

# Install python envir 
RUN apt-get update -y --fix-missing
RUN apt-get install -y ffmpeg
RUN apt-get install -y build-essential cmake pkg-config \
                    libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev \
                    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
                    libxvidcore-dev libx264-dev \
                    libgtk-3-dev \
                    libatlas-base-dev gfortran \
                    libboost-all-dev \
                    python3 python3-dev python3-numpy

RUN apt-get install -y wget vim python3-tk python3-pip

# Install git
RUN apt-get install -y git

# Install dlib envir
RUN apt-get install build-essential cmake pkg-config
RUN apt-get install libx11-dev libatlas-base-dev
RUN apt-get install libgtk-3-dev libboost-python-dev

# Install Zbar
RUN apt-get install -y build-essential libzbar-dev 

# Install tesseract
RUN  apt-get install python-software-properties -y 
RUN  apt-get install software-properties-common -y 
RUN  add-apt-repository ppa:alex-p/tesseract-ocr 
RUN  apt-get update -y --fix-missing
RUN  apt-get install tesseract-ocr -y

# Install dlib 19.13
RUN wget http://dlib.net/files/dlib-19.13.tar.bz2 \
    && tar xvf dlib-19.13.tar.bz2
RUN cd dlib-19.13 \
    && mkdir build \
    && cd build \
    && cmake .. \
    && cmake --build . --config Release \
    && make install \
    && ldconfig \
    && cd .. \
    && pkg-config --libs --cflags dlib-1 \
    && python3 setup.py install \
    && cd .. \
    && rm /dlib-19.13.tar.bz2

# Install project python lib
ADD $PWD/requirements.txt /requirements.txt
RUN pip3 install -r /requirements.txt

# Install google cloud
RUN pip3 install --upgrade google-cloud

# Git clone MLServer project
RUN git clone https://github.com/r92546024/MLServer.git  /var/log/RUN/

WORKDIR /var/log/RUN/
# VOLUME ["/var/log/RUN"]


##Run SSH#####################
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:fortinet' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
#CMD ["/usr/sbin/sshd", "-D"]
EXPOSE 22
##############################


#
# Execute Web Server
#CMD ["python3","./MLServer_Upload.py"] 

##################Other Install##############################
## Need manully build google json auth file and 
## run the following to Install Zbar
##  RUN apt-get update \
##    && apt-get install -y build-essential libzbar-dev  \
##    && pip3 install zbar
##################RUN the system#############################
## RUN cd /var/log/MLServer \
##     && python3 MLServer_Upload.py >> MLServer_Upload.log
#############################################################

