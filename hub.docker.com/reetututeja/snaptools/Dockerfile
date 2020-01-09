FROM ubuntu:18.04

RUN apt-get update --fix-missing
RUN apt-get install -y tzdata software-properties-common && apt-add-repository universe && apt-get update --fix-missing
RUN apt-get install -y python r-base python-pip 

RUN pip install snaptools
