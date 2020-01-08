FROM docker.elastic.co/kibana/kibana-oss:6.6.2

RUN bin/kibana-plugin install https://github.com/sivasamyk/logtrail/releases/download/v0.1.31/logtrail-6.6.2-0.1.31.zip

COPY logtrail.json /usr/share/kibana/plugins/logtrail/logtrail.json
