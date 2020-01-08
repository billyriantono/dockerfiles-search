FROM docker.elastic.co/kibana/kibana-oss:6.2.4
RUN ./bin/kibana-plugin install https://github.com/sivasamyk/logtrail/releases/download/v0.1.27/logtrail-6.2.4-0.1.27.zip
COPY logtrail.json ./plugins/logtrail/logtrail.json
