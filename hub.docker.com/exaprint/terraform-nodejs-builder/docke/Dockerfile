FROM node:10

RUN apt-get update \
  && apt-get install -y \
    zip \
    python3-pip \
    ghostscript \
    mysql-client \
  && pip3 install awscli --upgrade \
  && npm i -g npm serverless sonarqube-scanner nyc mocha mocha-multi-reporters mocha-sonarqube-reporter mocha-junit-reporter

ENTRYPOINT ["/bin/bash", "-c"]
