FROM docker.elastic.co/beats/metricbeat:6.6.0
# Copy our custom configuration file
COPY . /usr/share/metricbeat/
USER root
RUN chown -R root /usr/share/metricbeat/
RUN chmod -R go-w /usr/share/metricbeat/
