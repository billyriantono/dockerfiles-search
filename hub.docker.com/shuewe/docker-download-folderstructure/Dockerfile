FROM ubuntu:latest

MAINTAINER Stephan Hüwe (shuewe87@gmail.com)

ADD git-folder-scripts git-folder-scripts
ADD folder-system-definitions folder-system-definitions

#Install python3.7
RUN apt-get -y update
RUN apt-get install vim git wget -y
RUN apt-get install software-properties-common swig -y
RUN apt-get install python3.7 python3.7-dev build-essential python3-pip gfortran libgfortran5 libatlas3-base -y
RUN ln -s -f /usr/bin/python3.7 /usr/bin/python
RUN python -m pip install --upgrade pip
RUN apt-get install python3-numpy -y
RUN apt-get install portaudio19-dev -y
RUN apt-get install python3-scipy -y
RUN apt-get install python3-h5py -y
RUN printf "[global]\nextra-index-url=https://www.piwheels.org/simple">/etc/pip.conf
RUN apt-get install libatlas-base-dev -y
RUN python -m pip install tensorflow

RUN ["chmod", "+x", "/git-folder-scripts/start.sh"]

ENTRYPOINT ["/git-folder-scripts/start.sh"] 
