FROM node:10-jessie
RUN apt-get update && \
apt-get install python-dev -y && \
apt-get clean
RUN npm install -g serverless@1.54.0 json@9.0.6 aws-cdk@1.18
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
RUN python get-pip.py
RUN pip install awscli --upgrade