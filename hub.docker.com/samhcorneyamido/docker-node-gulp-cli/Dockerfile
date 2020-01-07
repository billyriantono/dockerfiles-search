FROM node:8
RUN npm install -g gulp-cli && \
    apt-get update && \
    apt-get install -y python && \
    apt-get install -y python-dev && \
    apt-get install -y python-pip && \
    pip install awscli --upgrade
