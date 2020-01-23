FROM ubuntu:17.10
MAINTAINER Conrad Jones "cjones@turboit.co.uk"

RUN apt-get update
RUN apt-get install -y gcc g++ ccache git make binutils cmake xvfb
RUN apt-get install -y libasound2-dev libaubio-dev portaudio19-dev libsndfile1-dev
RUN apt-get install -y qt5-default 
RUN apt-get install -y libboost1.63-all-dev
RUN mkdir /root/.ssh
