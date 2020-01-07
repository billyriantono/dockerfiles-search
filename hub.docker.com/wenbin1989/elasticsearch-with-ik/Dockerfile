FROM elasticsearch:1.7
MAINTAINER Wenbin Wang <wenbin1989@gmail.com>

COPY plugins /usr/share/elasticsearch/plugins
RUN chown -R elasticsearch.elasticsearch /usr/share/elasticsearch/plugins
COPY ik /usr/share/elasticsearch/config/ik
RUN { \
        echo "index:"; \
        echo "  analysis:"; \
        echo "    analyzer:"; \
        echo "      ik:"; \
        echo "          alias: [news_analyzer_ik,ik_analyzer]"; \
        echo "          type: org.elasticsearch.index.analysis.IkAnalyzerProvider"; \
        echo "index.analysis.analyzer.default.type: \"ik\""; \
    } >> /usr/share/elasticsearch/config/elasticsearch.yml

