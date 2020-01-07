FROM sebp/elk

RUN /opt/kibana/bin/kibana-plugin install http://unpkg.com/@streamplace/logtrail@0.1.28/build/logtrail-0.1.28.zip
ADD logtrail.json /opt/kibana/plugins/logtrail/logtrail.json
