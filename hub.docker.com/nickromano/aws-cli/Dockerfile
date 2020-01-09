# docker build . -t aws-cli -f Dockerfile-aws-cli
FROM python:2.7

# https://github.com/aws/aws-cli/issues/1957
RUN apt-get update && apt-get install -y \
    less \
    groff

RUN pip install awscli

