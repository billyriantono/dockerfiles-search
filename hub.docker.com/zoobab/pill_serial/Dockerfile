FROM debian:jessie-slim
MAINTAINER Benjamin Henrion <zoobab@gmail.com>
LABEL Description="3x USB-serial ports with a STM32 Bluepill board"

RUN DEBIAN_FRONTEND=noninteractive apt-get update -y -q && apt-get install -y -q sudo make python gcc-arm-none-eabi git-core libnewlib-arm-none-eabi

ENV user pillserial
RUN useradd -d /home/$user -m -s /bin/bash $user
RUN echo "$user ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$user
RUN chmod 0440 /etc/sudoers.d/$user

USER $user
WORKDIR /home/$user
RUN mkdir -pv code
COPY . ./code/
RUN sudo chown $user.$user -R /home/$user/code
WORKDIR /home/$user/code/
RUN make all
