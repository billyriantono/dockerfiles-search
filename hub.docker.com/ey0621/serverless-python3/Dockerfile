FROM circleci/python:3.6.5

RUN sudo apt-get update \
    && sudo apt-get install -y \
        curl \
        shellcheck \
    && sudo apt-get clean \
    && sudo rm -rf /var/lib/apt/lists/*

RUN sudo pip install \
    awscli \
    pipenv

RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash - \
    && sudo apt-get install -y nodejs

RUN sudo npm install -g npm \
    && sudo npm install -g serverless
