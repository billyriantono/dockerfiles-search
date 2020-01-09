FROM ubuntu:16.04
MAINTAINER Ephraim Rothschild
RUN mkdir -p /compilebox/usercode && chmod -R 777 /compilebox/usercode
# Update the repository sources list
RUN apt-get update -y
RUN apt-get install -y software-properties-common
RUN add-apt-repository universe
RUN apt-get update -y

# Set Timezone
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#For C/C++
RUN apt-get install -y libc6-dev
RUN apt-get install -y gcc
RUN apt-get install -y g++
RUN apt-get install -y libboost-all-dev
RUN apt-get install -y aptitude
RUN aptitude search boost



# For Objective C
RUN apt-get install -y clang
RUN apt-get install -y gobjc
RUN apt-get install -y gnustep
RUN apt-get install -y gnustep-devel &&  sed -i 's/#define BASE_NATIVE_OBJC_EXCEPTIONS     1/#define BASE_NATIVE_OBJC_EXCEPTIONS     0/g' /usr/include/GNUstep/GNUstepBase/GSConfig.h

RUN apt-get install -y sudo
RUN apt-get install -y bc