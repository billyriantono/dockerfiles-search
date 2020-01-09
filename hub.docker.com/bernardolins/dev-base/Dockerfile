#### This is a base image containing some basic
#### software needed in almost every development project
FROM debian:latest

MAINTAINER bernardolins28@gmail.com

RUN apt-get update -y
#### installing make, curl, wget
RUN apt-get install -y make curl wget

#### installing gcc and g++
RUN apt-get -y install -y gcc g++

#### installing git
RUN apt-get install -y git

#### installing ssh and sshd
RUN apt-get install -y openssh-client openssh-server

#### installing cmake
RUN apt-get install -y cmake

#### installing some libs
RUN apt-get install -y build-essential python-dev autotools-dev libicu-dev libbz2-dev 

### installing some zip tools
RUN apt-get install -y unzip bzip2
