FROM node:5.11.0

RUN apt-get -y update
RUN apt-get -y install zip
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python2.7 get-pip.py
RUN pip install boto3==1.3.0