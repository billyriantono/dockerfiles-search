# Docker image for AWS Ubuntu Emulation
FROM ubuntu:bionic

RUN apt-get update && apt-get install -y sudo && \
  # Create ubuntu user
  groupadd -g 1000 ubuntu && \
  useradd -g ubuntu -G sudo -m -s /bin/bash ubuntu && \
  echo 'ubuntu:ubuntu' | chpasswd && \
  # Allow ubuntu user to sudo
  echo 'Defaults visiblepw' >> /etc/sudoers && \
  echo 'ubuntu ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set login user to ubuntu
USER ubuntu
