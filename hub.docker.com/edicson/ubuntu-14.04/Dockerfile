FROM ubuntu:14.04

CMD ["echo","Creating Entsia Docker Image for Ubuntu 14.04 !!!"]

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget && \
  apt-get install -y curl && \
  apt-get install -y apt-transport-https && \
  apt-get install -y apt-utils && \
  rm -rf /var/lib/apt/lists/*

# Add files.
ADD root/.bashrc /root/.bashrc
ADD root/.gitconfig /root/.gitconfig
ADD root/.scripts /root/.scripts

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

CMD ["echo","Finishing configuration, Entsia Docker Image for Ubuntu 14.04 is ready to use!!!"]

# Define default command.
CMD ["bash"]
