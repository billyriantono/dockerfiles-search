FROM btooncall/centos7:devel

RUN mkdir -p /opt/ 2>/dev/null; 
WORKDIR /opt

RUN wget -q https://download.elastic.co/kibana/kibana/kibana-4.5.0-1.x86_64.rpm \
      && yum -y install /opt/kibana-4.5.0-1.x86_64.rpm \
      && rm -f /opt/kibana-4.5.0-1.x86_64.rpm \
      && yum clean all
      
RUN sed -i 's/^.*server.port:.*$/server.port: 5601/g' /opt/kibana/config/kibana.yml
RUN sed -i 's/^.*server.host:.*$/server.host: "0.0.0.0"/g' /opt/kibana/config/kibana.yml
RUN sed -i 's/^.*logging.dest:.*$/logging.dest: stdout/g' /opt/kibana/config/kibana.yml
RUN sed -i 's/^.*elasticsearch.url:.*$/elasticsearch.url: "http:\/\/elasticsearch:9200"/g' /opt/kibana/config/kibana.yml

EXPOSE 5601

WORKDIR /opt/kibana

ENTRYPOINT [ "bin/kibana" ]
