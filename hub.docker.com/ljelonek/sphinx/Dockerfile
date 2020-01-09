FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive

# Update apt-get sources AND install stuff
RUN apt-get update && \
    apt-get install -y -q python3-pip \
                          make 
    
RUN pip3 install sphinx sphinx-rtd-theme sphinxcontrib-httpdomain
