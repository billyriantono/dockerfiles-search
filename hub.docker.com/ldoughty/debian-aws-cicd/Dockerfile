FROM python:3.7-slim-buster

ARG CLI_VERSION=1.16.235

# This image is used in CICD pipelines, and therefore doesn't
# need the 250MB of extra packages for AWS documentation
# support
RUN pip3 install --no-cache-dir awscli==$CLI_VERSION

WORKDIR /tmp

CMD bash
