FROM debian:buster-slim
MAINTAINER Pawel Szczepaniak <krzyzakp@gmail.com>

RUN apt-get update && \ 
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -yq \ 
    python3 python3-distutils curl jq
RUN curl --silent --show-error -retry 5 \
    https://bootstrap.pypa.io/get-pip.py | python3
RUN pip3 install awscli
RUN curl https://amazon-ssm-us-east-1.s3.amazonaws.com/latest/debian_amd64/amazon-ssm-agent.deb \
    -o amazon-ssm-agent.deb && dpkg -i amazon-ssm-agent.deb && rm -f amazon-ssm-agent.deb
