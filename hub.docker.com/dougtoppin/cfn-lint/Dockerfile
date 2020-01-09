FROM ruby:2.3
LABEL maintainer "dougtoppin@gmail.com"
LABEL org.label-schema.vcs-url="https://github.com/dougtoppin/cfn-lint"
LABEL org.label-schema.description="AWS CloudFormation Linter from https://github.com/awslabs/cfn-python-lint"

RUN apt-get update && apt-get -y install python-setuptools python-dev build-essential
RUN easy_install pip
RUN pip install cfn-lint

WORKDIR /opt
ENTRYPOINT [ "/usr/local/bin/cfn-lint" ]
