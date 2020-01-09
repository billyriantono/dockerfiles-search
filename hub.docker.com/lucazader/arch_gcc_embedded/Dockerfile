FROM archlinux/base:latest
MAINTAINER Lucas Hutchinson <lucas.hutchinson@gmail.com>
LABEL Description="Image for building and debugging arm-embedded projects from git"
WORKDIR /work

ADD . /work

# Install any needed packages specified in requirements.txt
RUN pacman -Sy --noconfirm make cmake ninja git python openssh arm-none-eabi-gcc arm-none-eabi-newlib
