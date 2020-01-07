FROM balenalib/raspberrypi3
MAINTAINER Andrew Guterman <andrew@playpiper.com>

# QEMU shell hooks begin
RUN ["cross-build-start"]

# Update packages
RUN apt-get update

# Install build essentials
RUN apt-get install build-essential

# Install Git
RUN apt-get install git -y

# Install Python
RUN apt-get install python

# Install WiringPi
RUN apt-get install wiringpi -y

# Install NodeJS
ARG node_ver=v8.9.1
ARG node_dist=linux-armv7l
ARG node_full=node-$node_ver-$node_dist
ARG node_tar=$node_full.tar.xz

RUN apt-get install wget

RUN wget "https://nodejs.org/dist/$node_ver/$node_tar"
RUN mkdir /usr/local/lib/nodejs
RUN tar -xJvf "$node_tar" -C /usr/local/lib/nodejs
RUN mv "/usr/local/lib/nodejs/$node_full" "/usr/local/lib/nodejs/node-$node_ver"

ENV NODEJS_HOME "/usr/local/lib/nodejs/node-$node_ver/bin"
ENV PATH "$NODEJS_HOME:$PATH"

# Create directory
WORKDIR /usr/local/games/pipercode

# Copy files
COPY . /usr/local/games/pipercode/

# Build initial pass for package cache
ENV NPM_CONFIG_PREFIX "~/.npm-global"
RUN npm install

# QEMU shell hooks end
RUN ["cross-build-end"]
CMD ["bash"]
