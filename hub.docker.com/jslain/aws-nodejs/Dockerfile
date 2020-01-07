FROM node

RUN apt-get update && apt-get install -y\
      python \
      python-requests \
      python-pip \
      python-hglib \
      libpython-dev \
      unzip \
      zip

RUN rm -rf /usr/local/lib/python2.7/dist-packages/requests*

RUN pip install \
      awsebcli \
      awscli \
      --upgrade




