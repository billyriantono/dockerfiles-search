FROM docker.elastic.co/elasticsearch/elasticsearch:6.7.2
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install \
  --batch https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.7.2/elasticsearch-analysis-ik-6.7.2.zip \
  && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
