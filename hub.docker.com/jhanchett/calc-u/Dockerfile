FROM ubuntu:18.04

LABEL edu.uanet.jjh132-devops.url="https://github.com/UAComputerScience/dockerfile-JJH132/tree/ubuntu_18.04" \
	  edu.uanet.jjh132-devops.distro="ubuntu" \
	  edu.uanet.jjh132-devops.osversion="18.04" \
	  edu.uanet.jjh132-devops.architecure="x86_64"

# Update and install dependencies
RUN apt-get update -y && apt-get install -y \
    make \
    g++ \
    curl

# Download calculator source
ARG CALC_VERSION=v1.0
ARG CALC_URL=https://github.com/JJH132/DockerDemo/archive/${CALC_VERSION}.tar.gz
RUN curl -L $CALC_URL | tar xvz


# Extract the source 
#RUN tar xvzf ${CALC_VERSION}.tar.gz
RUN cd DockerDemo-1.0 && make

# create work directory
WORKDIR DockerDemo-1.0

# Start Calculator and run example
#RUN ./Calculator
#RUN 2 + 2 (4) / (5 * 7 - 2);\n 
#RUN quit\n
#RUN ./Calculator 2 + 2 (4) / (5 * 7 - 2); quit
#RUN ["./Calculator", "2 + 2 (4) / (5 * 7 - 2);", "quit"]
RUN curl --help
