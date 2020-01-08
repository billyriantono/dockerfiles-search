FROM  node:stretch

RUN apt-get update && \
    apt-get install -y -qq \
    python-pip \
    xvfb \
    firefox-esr && \
	pip install awsebcli && \
    pip install awscli && \
    apt-get clean
