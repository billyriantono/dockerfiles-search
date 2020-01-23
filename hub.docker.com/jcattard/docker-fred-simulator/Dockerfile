FROM ubuntu:latest
MAINTAINER jcattard

# Update aptitude with new repo
RUN apt-get update

# Install software
RUN apt-get install -y git make build-essential unzip python dos2unix

RUN useradd -ms /bin/bash -G staff user01
USER user01
WORKDIR /home/user01
RUN git clone https://github.com/PublicHealthDynamicsLab/FRED.git
ENV FRED_HOME /home/user01/FRED
ENV PATH $FRED_HOME/bin:$PATH
RUN . /home/user01/.profile
WORKDIR /home/user01/FRED
RUN make
