FROM ubuntu:xenial
MAINTAINER Marlon Cruz <marlon.c@thediary.com>

USER root

#========================================
# Dependencies
#========================================
RUN apt-get update && apt-get upgrade -y && apt-get install -y fontconfig curl build-essential g++ flex bison gperf ruby perl

RUN apt-get install -y libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev

RUN apt-get install -y libpng-dev libjpeg-dev python python-pip libx11-dev libxext-dev sudo

RUN apt-get install -y python-dev libtiff5-dev libjpeg8-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python-tk

#========================================
# Robot Framework and Selenium
#========================================
RUN pip install requests selenium robotframework robotframework-selenium2library robotframework-requests robotframework-sudslibrary robotframework-appiumlibrary pyhamcrest

RUN pip install Pillow robotframework-selenium2screenshots

#========================================
# Add normal user with passwordless sudo
#========================================
RUN sudo useradd robotuser --shell /bin/bash --create-home && sudo usermod -a -G sudo robotuser && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers && echo 'robotuser:secret' | chpasswd

CMD ["tail", "-f", "/dev/null"]
