FROM ubuntu:13.10
MAINTAINER bltgv

#Get tools
RUN apt-get update
RUN apt-get -y install libtool autoconf g++ gettext make git

#Clone patched mono
RUN git clone https://github.com/bltgv/mono

#Compile mono
RUN cd mono; ./autogen.sh --prefix /usr
RUN cd mono; make get-monolite-latest
RUN cd mono; make EXTERNAL_MCS="${PWD}/mcs/class/lib/monolite/gmcs.exe"
RUN cd mono; make

#Install mono
RUN cd mono; make install

#Remove mono build files
RUN rm -r /mono
