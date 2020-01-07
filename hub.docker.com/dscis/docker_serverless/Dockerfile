FROM node:8.5
RUN apt-get update && \
apt-get install python-dev -y && \
apt-get clean
RUN npm install -g serverless@1.21.1 && \
curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install awscli
