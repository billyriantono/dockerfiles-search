FROM debian:jessie
RUN apt-get update
RUN apt-get install -y python2.7-dev wget build-essential python curl
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -
RUN apt-get install --force-yes -y nodejs 

