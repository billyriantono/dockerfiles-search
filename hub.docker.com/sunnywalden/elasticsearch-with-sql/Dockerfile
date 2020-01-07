# base image
FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.4

# MAINTAINER
MAINTAINER sunnywalden@gmail.com

ENV ES_HOME /usr/share/elasticsearch

RUN mkdir -p ${ES_HOME}/node
ADD node-v10.15.3-linux-x64 ${ES_HOME}/node
RUN ls -la ./node
ENV NODE_HOME ${ES_HOME}/node
ENV PATH ${NODE_HOME}/bin:$PATH

RUN mkdir -p ${ES_HOME}/es-sql
COPY es-sql ${ES_HOME}/es-sql/

ADD elasticsearch-sql-5.6.4.0.zip /tmp
RUN ./bin/elasticsearch-plugin install file:///tmp/elasticsearch-sql-5.6.4.0.zip
USER root
WORKDIR ${ES_HOME}/es-sql/site-server
RUN npm install express --save
#ADD entrypoint.sh ${ES_HOME}/
RUN chown -R elasticsearch:elasticsearch ${ES_HOME}

USER elasticsearch
WORKDIR ${ES_HOME}
#CMD nohup sh -c './bin/elasticsearch && cd ./es-sql/site-server/ && node node-server.js &'
#ENTRYPOINT ["./entrypoint.sh"]

EXPOSE 9200
EXPOSE 9300
EXPOSE 8080 
