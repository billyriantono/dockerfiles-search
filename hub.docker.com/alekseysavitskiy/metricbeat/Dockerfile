FROM docker.elastic.co/beats/metricbeat:6.3.1
USER root
RUN find /usr/share/metricbeat/kibana/6/dashboard/ ! -name 'Metricbeat-docker-overview.json' -type f -exec rm -f {} +
