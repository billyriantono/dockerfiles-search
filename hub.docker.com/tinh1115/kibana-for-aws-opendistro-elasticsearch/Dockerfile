FROM amazon/opendistro-for-elasticsearch-kibana:0.7.0
COPY ./entrypoint.sh /
COPY ./kibana.yml /
RUN /usr/share/kibana/bin/kibana-plugin remove opendistro_security

ENTRYPOINT ["/bin/bash"]
USER root
WORKDIR /root
CMD ["/entrypoint.sh"]