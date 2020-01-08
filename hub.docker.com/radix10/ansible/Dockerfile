FROM ubuntu:18.04
MAINTAINER "admin@radix10.cn"

ARG USERNAME=ansible

# Install sudo and ansible
RUN apt-get update && apt-get install -y sudo ansible ssh

# Create user
RUN useradd -m -g users -G sudo -s /bin/bash $USERNAME

# Switch user
USER $USERNAME
WORKDIR /home/$USERNAME
