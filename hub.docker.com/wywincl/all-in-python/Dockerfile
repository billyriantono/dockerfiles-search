FROM python:2.7.12

MAINTAINER john.wang <wywincl@126.com>

#=========================================
# Install robotframework and it's library
#=========================================
RUN pip install -U robotframework
RUN pip install -U robotframework-selenium2library
RUN pip install -U requests
RUN pip install -U requests-toolbelt
RUN pip install -U robotframework-requests
RUN pip install -U robotframework-pabot

#=========================================
# Install aws 
#=========================================
RUN pip install -U boto3
RUN pip install -U awscli

#=========================================
# Install bs4 
#=========================================
RUN pip install -U beautifulsoup4

#============
# workspace
#============
RUN mkdir /etc/robot
VOLUME /etc/robot
WORKDIR /etc/robot
