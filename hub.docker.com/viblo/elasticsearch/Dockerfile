ARG ELASTICSEARCH_VERSION

FROM elasticsearch:${ELASTICSEARCH_VERSION}

ARG ELASTICSEARCH_VERSION

RUN elasticsearch-plugin install --batch analysis-kuromoji \
    && elasticsearch-plugin install --batch analysis-icu \
    && elasticsearch-plugin install --batch https://github.com/sun-asterisk-research/elasticsearch-analysis-vi/releases/download/v1.0.0/analysis-vi-1.0.0-es${ELASTICSEARCH_VERSION}.zip
