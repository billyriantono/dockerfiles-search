FROM kibana:latest

RUN /opt/kibana/bin/kibana plugin --install elastic/sense/latest
RUN /opt/kibana/bin/kibana plugin --install elasticsearch/marvel/2.3.4
RUN chown -R kibana:kibana /opt/kibana
