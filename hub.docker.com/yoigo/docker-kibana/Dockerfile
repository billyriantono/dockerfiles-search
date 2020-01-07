FROM docker.elastic.co/kibana/kibana:5.6.0

# Remove xpack support
RUN bin/kibana-plugin remove x-pack

# Install logtrail plugin
RUN kibana-plugin install https://github.com/sivasamyk/logtrail/releases/download/v0.1.21/logtrail-5.6.0-0.1.21.zip