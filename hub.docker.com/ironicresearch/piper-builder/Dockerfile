FROM ubuntu:16.04
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y git binutils
RUN apt-get update && apt-get install -y wget zip
RUN apt-get update && apt-get install -y curl ca-certificates
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash
RUN apt-get install -y --no-install-recommends git-lfs
RUN git lfs install
WORKDIR /home/piper
ARG REPO_USER
ENV REPO_USER $REPO_USER
RUN git clone http://${REPO_USER}github.com/buildwithpiper/piper-builder -b piper2
WORKDIR piper-builder/piper2
RUN git clone --depth=1 https://${REPO_USER}github.com/buildwithpiper/piper-story.git -b master
ENV RASPBIAN_LATEST raspbian-2018-06-29/2018-06-27-raspbian-stretch.zip
RUN wget -O raspbian_latest https://downloads.raspberrypi.org/raspbian/images/$RASPBIAN_LATEST
CMD ./build.sh
