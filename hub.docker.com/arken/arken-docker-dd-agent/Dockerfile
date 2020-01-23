FROM datadog/docker-dd-agent

MAINTAINER Damien Metzler <dmetzler@nuxeo.com>
ADD docker.yaml /etc/dd-agent/conf.d/docker.yaml
CMD ["/usr/local/bin/run-dd-agent.sh"]
