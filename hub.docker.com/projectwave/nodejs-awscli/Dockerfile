FROM node:10.15.0

ENV AWS_CLI_VERSION 1.16.80

RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install -y libpython-dev \
        python-pip \
        jq \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        software-properties-common \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && apt-get update -y \
    && apt-get install -y docker-ce \
    && pip install -q awscli==${AWS_CLI_VERSION} --upgrade \
    && pip install j2 \
    && apt-get clean