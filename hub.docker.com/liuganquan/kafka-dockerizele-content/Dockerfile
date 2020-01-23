FROM debian:stretch

MAINTAINER Milo Casagrande <milo.casagrande@linaro.org>
LABEL Version="1.0" Description="Run the git://ci broker"

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get clean && apt-get update -qq && apt-get install -qq -y --no-install-recommends \
    git \
    python3 \
    python3-httplib2 \
    python3-oauth2client \
    python3-pip \
    python3-pyasn1 \
    python3-requests-oauthlib \
    python3-rsa \
    python3-tzlocal \
    python3-virtualenv \
    python3-yaml \
    python3-zmq \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /srv/gitci-broker-env
RUN cd /srv ; git clone https://github.com/linaro-product/gitci-broker.git

ENV PYTHONUSERBASE /srv/gitci-broker-env
RUN pip3 install -q -r /srv/gitci-broker/requirements.txt --user

EXPOSE 5555 5556

WORKDIR /srv/gitci-broker
CMD ["python3", "broker.py", "--debug"]
