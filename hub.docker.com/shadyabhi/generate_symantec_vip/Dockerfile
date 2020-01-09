FROM phusion/baseimage

RUN apt-get update

RUN apt-get install -y python-pip && python -m pip install --upgrade pip setuptools && python -m pip install python-vipaccess;

ADD generate.py /opt/generate.py

RUN chmod a+x /opt/generate.py && /opt/generate.py
