FROM node:6.9.2
MAINTAINER James Chevalier <james.chevalier@commonmedia.com>

RUN apt-get update && apt-get install -y --no-install-recommends python python-dev wget ca-certificates

RUN wget https://bootstrap.pypa.io/get-pip.py && python get-pip.py && rm get-pip.py

RUN pip install awscli --upgrade --ignore-installed six
