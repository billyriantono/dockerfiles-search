FROM ubuntu:18.04


# install python and git
RUN apt-get update \
    && apt-get install -y python3.6 python3-pip \
	&& apt-get install -y git

	
# get latest cvlib from github	
WORKDIR /
RUN git clone https://github.com/arunponnusamy/cvlib


# install cvlib and dependencies
WORKDIR /cvlib
RUN pip3 install -r requirements.txt
RUN pip3 install cvlib
RUN apt install -y libsm6 libxext6 libxrender-dev


# cleanup
WORKDIR /cvlib/examples
RUN apt-get remove -y git python3-pip
