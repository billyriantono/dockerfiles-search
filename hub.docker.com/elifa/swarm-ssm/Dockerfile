FROM debian:jessie

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -yq lsb-release curl

ENV AGENT_URL https://s3.amazonaws.com/ec2-downloads-windows/SSMAgent/latest/debian_amd64/amazon-ssm-agent.deb

RUN curl ${AGENT_URL} -o amazon-ssm-agent.deb && \
    dpkg -i amazon-ssm-agent.deb && \
    rm -f amazon-ssm-agent.deb

WORKDIR /opt/amazon/ssm/
CMD ["amazon-ssm-agent", "start"]