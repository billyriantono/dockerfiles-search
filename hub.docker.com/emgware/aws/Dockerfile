FROM node:lts

RUN apt-get update && \
    apt-get -y install apt-transport-https && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get -y install yarn python python-pip python-dev groff
RUN ln -sf /usr/bin/yarn /usr/local/bin/yarn

RUN pip install awscli

RUN npm install -g @aws-amplify/cli serverless

COPY .aws /opt/.aws

ENV AWS_CONFIG_FILE /opt/.aws/config
ENV AWS_SHARED_CREDENTIALS_FILE /opt/.aws/credentials
