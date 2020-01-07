FROM ubuntu:latest

ENV home=/root
WORKDIR ${home}

RUN mkdir ${home}/download
RUN mkdir ${home}/kaggle

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install build-essential libsqlite3-dev libreadline6-dev libgdbm-dev zlib1g-dev libbz2-dev sqlite3 tk-dev zip libssl-dev libjpeg-dev wget python-matplotlib

RUN apt-get -y install python-dev
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py

RUN pip install numpy pandas Pillow
RUN pip install --upgrade https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl
