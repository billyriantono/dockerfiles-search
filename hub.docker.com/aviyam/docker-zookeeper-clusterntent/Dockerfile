FROM aveu/docker-ng-node-chrome:latest

# Set UTF-8 locale

ENV LANG C.UTF-8

# Install Python3.x

RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends python3 python3-dev

RUN python3 --version

# Install PIP

RUN curl -O https://bootstrap.pypa.io/get-pip.py \
    && python3 get-pip.py --user

RUN ~/.local/bin/pip --version

# Install EB CLI

RUN ~/.local/bin/pip install --upgrade pip

RUN ~/.local/bin/pip install --upgrade awscli

RUN ~/.local/bin/pip install --upgrade awsebcli

RUN eb --version
