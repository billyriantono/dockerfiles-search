FROM node:8-jessie
RUN apt-get update && \
apt-get install python-dev -y && \
apt-get clean
RUN npm install -g serverless@1.42.3 json@9.0.6
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
RUN python get-pip.py
RUN pip install awscli --upgrade