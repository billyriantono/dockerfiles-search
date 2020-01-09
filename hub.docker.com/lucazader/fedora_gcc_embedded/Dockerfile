
FROM fedora:latest
MAINTAINER Lucas Hutchinson <lucas.hutchinson@gmail.com>
LABEL Description="Image for building and debugging arm-embedded projects from git"
WORKDIR /work

ADD . /work

# Install any needed packages specified in requirements.txt
RUN dnf -y install make cmake ninja-build git python openssh arm-none-eabi-newlib arm-none-eabi-gcc
