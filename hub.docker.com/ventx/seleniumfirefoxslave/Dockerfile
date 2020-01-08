FROM selenium/node-firefox:3.5.3-boron

USER root

RUN apt-get update && apt-get install -y \
  python3-pip && \
  pip3 install selenium 

USER seluser
WORKDIR work
