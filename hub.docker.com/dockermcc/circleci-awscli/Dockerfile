FROM circleci/node:10.15.3-stretch
MAINTAINER Greg Barry "gregory.paul.barry@gmail.com"

USER root

# Update Apt and Install packages
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y \
    python3 python3-pip python3-setuptools groff less vim libpoppler-qt5-dev libcairo2-dev && \
    pip3 install --upgrade pip && \
    apt-get clean

# Install AWS CLI
RUN pip3 --no-cache-dir install awscli

# End on shell
RUN ["/bin/bash"]

