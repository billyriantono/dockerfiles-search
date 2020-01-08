FROM node:6.11.1
MAINTAINER Rahul Shukla <shukla2009@gmail.com>
RUN apt-get update
RUN apt-get -y install libpython-dev python-pip 
RUN pip install awscli --upgrade --user
RUN echo "export PATH=/root/.local/bin:$PATH" >> /root/.bashrc