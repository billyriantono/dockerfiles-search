FROM centos:7
MAINTAINER Steve Bargelt

# Install Essentials
RUN yum update -y && \
    yum clean all
	
RUN yum install -y git && \
    yum install -y wget && \
        yum install -y java-1.8.0-openjdk && \
        yum install -y sudo && \
        yum install -y ftp && \ 
        yum install -y unzip && \
        yum install -y maven && \
        yum clean all	

RUN wget http://nodejs.org/dist/v8.5.0/node-v8.5.0-linux-x64.tar.gz
RUN sudo tar --strip-components 1 -xzvf node-v* -C /usr/local
RUN yum install -y make gcc*

# Install Allure
RUN wget https://github.com/allure-framework/allure1/releases/download/allure-core-1.5.2/allure-commandline.zip
#RUN wget https://dl.bintray.com/qameta/generic/io/qameta/allure/allure/2.3.5/allure-2.3.5.zip
RUN unzip allure-commandline.zip -d /usr/local/bin/allure

# Install Powershell
RUN wget http://tinyurl.com/hua9mtm 
RUN mv hua9mtm powershell.rpm 
RUN sudo yum install -y powershell.rpm

# Create Jenkins User
RUN useradd jenkins -m -s /bin/bash

RUN chown -R jenkins /home/jenkins
RUN chgrp -R jenkins /home/jenkins

# Add the jenkins user to sudoers
RUN echo "jenkins    ALL=(ALL)    ALL" >> etc/sudoers

# Set Name Servers
COPY /files/resolv.conf /etc/resolv.conf
