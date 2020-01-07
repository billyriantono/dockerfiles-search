FROM python:2-alpine

MAINTAINER Brian Dwyer

ENV CFN_SRC https://s3.amazonaws.com/cloudformation-examples/aws-cfn-bootstrap-latest.tar.gz

# Update PIP & Install PIPEnv
RUN python -m pip install --upgrade pip \
    && pip install ${CFN_SRC}\
    && rm -rf ~/.cache/pip
