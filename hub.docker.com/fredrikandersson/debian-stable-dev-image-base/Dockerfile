# Docker image containing generic tools for development, based on Debian latest (stable).

FROM debian:stable-20190910

# Basic build/development tools
RUN apt-get update --quiet --yes && apt-get install --quiet --yes git vim wget curl

# Install Git LFS
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get install --quiet --yes git-lfs
RUN git lfs install

# Copy bashrc file
COPY .bashrc root/
