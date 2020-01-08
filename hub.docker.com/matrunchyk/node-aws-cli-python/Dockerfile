FROM node:10.12.0

MAINTAINER Serhii Matrunchyk <serhii@digitalidea.studio>

RUN apt-get update && apt-get install -y \
    python-dev xvfb libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2

RUN mkdir -p /root/.cache/Cypress
RUN npm i -g cypress  --unsafe-perm=true --allow-root

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    pip install awscli
