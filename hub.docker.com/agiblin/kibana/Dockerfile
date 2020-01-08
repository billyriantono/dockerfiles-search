FROM kibana:4.4

RUN gosu kibana kibana plugin --install elasticsearch/marvel/2.2.1
RUN gosu kibana kibana plugin --install elastic/sense
RUN gosu kibana kibana plugin --install elastic/timelion
