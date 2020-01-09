FROM ubuntu:18.04

RUN mkdir /build

WORKDIR /build

RUN apt-get update && apt-get install -y curl ca-certificates

COPY amazon-cloudwatch-agent.deb /build/
RUN dpkg -i amazon-cloudwatch-agent.deb

# Simplified version of agent-ctl script. In docker, no systemctl-related command needed
COPY amazon-cloudwatch-agent-ctl /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl
COPY config.json /opt/aws/amazon-cloudwatch-agent/bin/config.json
COPY entry-point.sh .

ENTRYPOINT ["/build/entry-point.sh"]
