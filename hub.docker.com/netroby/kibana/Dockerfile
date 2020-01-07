FROM kibana
RUN cd /opt/kibana; \
        ./bin/kibana plugin -i marvel --url https://download.elasticsearch.org/elasticsearch/marvel/marvel-2.3.3.tar.gz  ;\
        ./bin/kibana plugin -i elastic/sense; \
        ./bin/kibana plugin -i elastic/timelion;
RUN chown -R kibana:kibana /opt/kibana
ENV NODE_OPTIONS " --max_old_space_size=128 "
ENV TERM xterm
