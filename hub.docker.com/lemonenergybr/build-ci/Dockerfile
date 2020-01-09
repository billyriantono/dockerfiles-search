FROM node:12

RUN apt-get update \
  && apt-get install -y \
    zip \
    python3-pip \
  && pip3 install awscli --upgrade \
  && npm i -g npm serverless sonarqube-scanner nyc mocha mocha-multi-reporters mocha-sonarqube-reporter mocha-junit-reporter jest

ENV NODE_ENV production

ENTRYPOINT ["/bin/bash", "-c"]
