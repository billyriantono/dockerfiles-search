FROM gcr.io/google_containers/fluentd-elasticsearch:1.20
MAINTAINER Jason Wen <zhenshan_wen@bmc.com>

RUN cp /etc/td-agent/td-agent.conf /etc/td-agent/td-agent-default.conf

COPY td-agent.conf /etc/td-agent/td-agent.conf