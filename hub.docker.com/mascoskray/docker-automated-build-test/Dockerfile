FROM ubuntu:18.04
MAINTAINER MascoSkray <MascoSkray@gmail.com>
ARG CLONE_ADDFLAG

#Update apt and install git
RUN apt-get update && apt-get install -y git
#Clone the latest UOJ Community verison to local
RUN echo "CL FLAG=${CLONE_ADDFLAG}" && cd ~ && git clone https://github.com/UniversalOJ/UOJ-System.git --depth 1 --single-branch ${CLONE_ADDFLAG}
