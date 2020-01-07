FROM node:8.10
MAINTAINER Nick Cousins <nick.cousins@relative.ie>

RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list
RUN apt-get update && apt-get install -y python-pip libpython-dev zip
RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
RUN python get-pip.py
RUN pip install awscli
RUN pip install boto3
RUN npm install serverless typescript serverless-domain-manager aws-cli -g

CMD /bin/bash
