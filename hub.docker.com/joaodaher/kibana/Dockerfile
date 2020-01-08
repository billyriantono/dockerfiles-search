FROM kibana:5

RUN kibana-plugin install x-pack

ADD ./config/kibana.yml /etc/kibana/kibana.yml

RUN chown -R kibana /usr/share/kibana/optimize/