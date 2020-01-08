FROM visyond/jelastic

RUN apt-get update  -y && apt-get install -y wget apt-transport-https gnupg2 && \
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | apt-key add - &&\
    echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list && \
    apt-get update

RUN curl -sL https://deb.nodesource.com/setup_10.x > /tmp/nodesource_setup.sh \
 && bash /tmp/nodesource_setup.sh \
 && rm /tmp/nodesource_setup.sh \
 && apt-get update \
 && apt-get install -y --no-install-recommends nodejs 

RUN apt-get install -y default-jre procps python-pip
RUN apt-get install -y elasticsearch kibana apm-server logstash
RUN apt-get install -y zip 
RUN pip install "elastalert>=0.2.0b" && wget https://github.com/bitsensor/elastalert/archive/master.zip -O /tmp/elasalert-server.zip && unzip  /tmp/elasalert-server.zip -d /opt/elastalert-server && cd /opt/elastalert-server/elastalert-master && npm install --production 
COPY config.json /opt/elastalert-server/elastalert-master/config/config.json

RUN mkdir /etc/elk

RUN \
  mv /etc/elasticsearch/ /etc/elk && ln -s /etc/elk/elasticsearch/ /etc/elasticsearch && \
  mv /etc/kibana/ /etc/elk && ln -s /etc/elk/kibana/ /etc/kibana && \
  mv /etc/apm-server/ /etc/elk && ln -s /etc/elk/apm-server/ /etc/apm-server && \
  mv /etc/logstash/ /etc/elk && ln -s /etc/elk/logstash/ /etc/logstash && \
  mkdir -p /etc/elk/elasalert/rules && ln -s /etc/elk/elasalert/rules /usr/local/bin/rules &&\
  ln -s /etc/elk/elasalert/config.yaml /usr/local/bin/config.yaml

COPY start /start
COPY config.yaml /etc/elk/elasalert/config.yaml
COPY elastalert-kibana-plugin-1.0.4-7.1.1.zip /tmp/elastalert-kibana-plugin-1.0.4-7.1.1.zip

RUN /usr/share/kibana/bin/kibana-plugin install file:///tmp/elastalert-kibana-plugin-1.0.4-7.1.1.zip

VOLUME /etc/elk
EXPOSE 5601
EXPOSE 9200
EXPOSE 8200
ENTRYPOINT /start

