FROM node:10-slim
RUN apt-get update 
RUN apt-get install -y jq zip build-essential python2.7 python2.7-dev git
RUN ln /usr/bin/python2.7 /usr/bin/python2 
RUN curl -O https://bootstrap.pypa.io/get-pip.py && python2.7 get-pip.py && rm get-pip.py
RUN pip install awscli
