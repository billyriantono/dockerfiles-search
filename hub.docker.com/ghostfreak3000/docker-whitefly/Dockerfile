FROM ubuntu:16.04

# ------------------------------------------------------

# --- Update Ubuntu

RUN apt-get update 

# ------------------------------------------------------

# --- Install Utility Programs

RUN apt-get install -y python python-dev curl build-essential python-opencv

# ------------------------------------------------------


# --- Install pip

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python get-pip.py

# ------------------------------------------------------

# --- Install clipper

RUN pip install clipper_admin

# ------------------------------------------------------

# --- Install docker

# RUN apt-get -y install apt-transport-https ca-certificates curl software-properties-common
# RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
# RUN apt-key fingerprint 0EBFCD88
# RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
# RUN apt-get update
# RUN apt-get -y install docker-ce

# ------------------------------------------------------


# --- Clean up

RUN apt-get clean

# ------------------------------------------------------
