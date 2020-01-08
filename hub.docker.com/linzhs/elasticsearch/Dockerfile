FROM elasticsearch:7.3.1

LABEL author="scottlin"

ENV ELASTICSEARCH_VERSION=7.3.1

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-nori
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-kuromoji
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-smartcn
RUN sh -c '/bin/echo -e "y" /usr/share/elasticsearch/bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${ELASTICSEARCH_VERSION}/elasticsearch-analysis-ik-${ELASTICSEARCH_VERSION}.zip'
RUN sh -c '/bin/echo -e "y" /usr/share/elasticsearch/bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v${ELASTICSEARCH_VERSION}/elasticsearch-analysis-pinyin-${ELASTICSEARCH_VERSION}.zip'
RUN sh -c '/bin/echo -e "y" /usr/share/elasticsearch/bin/elasticsearch-plugin install https://github.com/duydo/elasticsearch-analysis-vietnamese/releases/download/v${ELASTICSEARCH_VERSION}/elasticsearch-analysis-vietnamese-${ELASTICSEARCH_VERSION}.zip'

# docker run -d --name elasticsearch-scott --net elk -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch-scott