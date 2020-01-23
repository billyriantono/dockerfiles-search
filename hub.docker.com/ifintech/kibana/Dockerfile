FROM kibana:5.5.1

RUN kibana-plugin install https://github.com/sivasamyk/logtrail/releases/download/v0.1.18/logtrail-5.5.1-0.1.18.zip
COPY logtrail.json /usr/share/kibana/plugins/logtrail/logtrail.json