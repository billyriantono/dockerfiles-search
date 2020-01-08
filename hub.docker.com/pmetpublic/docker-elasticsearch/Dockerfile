FROM elasticsearch:5.2
MAINTAINER Keith Bentrup <kbentrup@magento.com>

RUN bin/elasticsearch-plugin install analysis-phonetic && \
    bin/elasticsearch-plugin install analysis-icu && \
    echo -e "script.inline: on\nscript.inline: on" >> /etc/elasticsearch/elasticsearch.yml
