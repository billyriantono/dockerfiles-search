FROM ubuntu:18.04
LABEL maintainer="Erik Nielsen <enielsen@urban-waterways.org>"

# env vars
ENV OPENCV4NODEJS_DISABLE_AUTOBUILD 1
ENV OPENCV_VERSION 3.4.3
ENV NODE_MAJOR_VERSION 10
ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/lib:${PATH}

# copy local files
COPY config/apt.conf /etc/apt/apt.conf
COPY build /build

# container setup
RUN ./build && rm /build
