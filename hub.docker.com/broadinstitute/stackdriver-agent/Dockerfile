FROM ubuntu:trusty

EXPOSE 8125/udp

RUN apt-get update && apt-get install -y curl && \
    curl -o /etc/apt/sources.list.d/stackdriver.list https://repo.stackdriver.com/trusty.list && \
    curl --silent https://app.stackdriver.com/RPM-GPG-KEY-stackdriver | apt-key add - && \
    apt-get -q update && apt-get install -y -q stackdriver-agent


COPY collectd-gcm.conf.tmpl /opt/stackdriver/collectd/etc/collectd.conf.tmpl
COPY run-agent.sh /usr/bin/run-agent.sh
COPY scripts/generate_stackdriver_labels.py /opt/stackdriver/collectd/etc/collectd.d/generate_stackdriver_labels.py

CMD ["run-agent.sh"]
