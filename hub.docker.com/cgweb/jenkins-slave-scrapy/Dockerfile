FROM centos:7
MAINTAINER Steve Bargelt

# Install Essentials
RUN yum update -y && \
    yum clean all
    
COPY /files/mongodb-org.repo /etc/yum.repos.d/mongodb-org.repo
#COPY /files/resolv.conf /etc/mongodborg.conf
COPY /files/resolv.conf /etc/resolv.conf

# Install Packages
RUN yum install -y git && \
    yum install -y wget && \
#    yum install -y centos-release-SCL && \
#    yum install -y python27 && \
	yum install -y java-1.8.0-openjdk && \
	yum install -y sudo && \
        yum install -y ftp && \ 
	yum install -y maven && \
	yum install mongodb-org -y && \
        #yum -y install python-pip && \
	yum clean all

RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py

## Python Family
#RUN yum install -qy python python-dev python-distribute python-pip ipython
RUN yum install -y gcc libffi-devel python-devel openssl-devel

## Selenium 
#RUN yum install -qy firefox xvfb 
#RUN pip install selenium pyvirtualdisplay
 
## AWS Python SDK
#RUN yum install boto3
 
## Scraping
#RUN pip install beautifulsoup4 requests 
#RUN yum install -y libffi-dev libxml2-dev libxslt-dev lib32z1-dev libssl-dev
 
## Scrapy
#RUN pip install lxml scrapy==0.24.6 scrapyjs
#RUN pip install service_identity
#RUN pip install PIL --allow-external PIL --allow-unverified PIL
RUN sudo pip install -U nltk
RUN sudo pip install -U numpy
RUN python -m nltk.downloader -d /usr/local/share/nltk_data averaged_perceptron_tagger stopwords punkt
#RUN python -m nltk.downloader stopwords
RUN pip install pillow python-slugify==1.1.4 boto==2.38.0 lxml requests parslepy dateparser service_identity pymongo==2.8 scrapy==0.24.6 scrapyjs
#RUN python import nltk

# Create Jenkins User
RUN useradd jenkins -m -s /bin/bash

RUN chown -R jenkins /home/jenkins
RUN chgrp -R jenkins /home/jenkins

# Add the jenkins user to sudoers
RUN echo "jenkins    ALL=(ALL)    ALL" >> etc/sudoers

# Set Name Servers
#COPY /files/resolv.conf /etc/resolv.conf
