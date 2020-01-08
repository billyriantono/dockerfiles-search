FROM alpine:latest

MAINTAINER Matthias Heindl <heindlmatthias@gmail.com>

# Install dependencies
RUN apk update
RUN apk add python
RUN apk add python-dev 
RUN apk add curl
RUN apk add zip
RUN apk add ca-certificates
RUN apk add nodejs nodejs-npm

# Install npm dependencies
RUN npm install -g npx

# Install AWS CLI
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py
RUN pip install awscli --upgrade six
