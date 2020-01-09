FROM ubuntu:16.04

ENV ENVIRONMENT=dev
ENV AWS_DEFAULT_REGION=us-west-1
ENV AWS_REGION=us-west-1

RUN apt-get update \
  && apt-get install -y python3 wget python3-pip \
  && pip3 install awscli \
  && wget https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 \
  && mkdir -p /opt/confd/bin \
  && mv confd-0.16.0-linux-amd64 /opt/confd/bin/confd \
  && chmod +x /opt/confd/bin/confd 

ENTRYPOINT ["/opt/confd/bin/confd"]
CMD ["-backend=ssm"]
