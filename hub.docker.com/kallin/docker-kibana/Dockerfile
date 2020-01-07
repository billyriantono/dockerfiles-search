FROM kibana:4.3.0

RUN /opt/kibana/bin/kibana plugin --install elastic/sense
RUN /opt/kibana/bin/kibana plugin --install elasticsearch/marvel/latest

RUN chown -R kibana:kibana /opt/kibana