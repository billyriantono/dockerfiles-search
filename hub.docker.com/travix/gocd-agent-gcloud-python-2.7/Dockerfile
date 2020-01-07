FROM travix/gocd-agent-gcloud:18.12.0

MAINTAINER Travix

# install packages
RUN apt-get update \
    && apt-get install -y \
        python \
        python-dev \
        python-setuptools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && easy_install pip

# upgrade pip
RUN pip install --upgrade pip pylint
