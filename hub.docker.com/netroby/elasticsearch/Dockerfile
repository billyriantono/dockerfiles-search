FROM elasticsearch

RUN cd /usr/share/elasticsearch ; \
        ./bin/plugin install -b license; \
        ./bin/plugin install -b marvel-agent; \
        ./bin/plugin install -b analysis-smartcn;
ENV TERM xterm
