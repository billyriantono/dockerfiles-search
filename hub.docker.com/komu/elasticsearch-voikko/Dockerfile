FROM dockerfile/elasticsearch

MAINTAINER juha.komulainen@evident.fi

# Install libvoikko
RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq libvoikko1

# Install Voikko's morpho-dictionary
RUN wget http://www.puimula.org/htp/testing/voikko-snapshot/dict-morpho.zip --quiet -O /tmp/dict-morpho.zip \
    && mkdir -p /usr/lib/voikko \
    && unzip -q /tmp/dict-morpho.zip -d /usr/lib/voikko \
    && rm /tmp/dict-morpho.zip

# Install the Voikko plugin for Elasticsearch
RUN /elasticsearch/bin/plugin --install fi.evident.elasticsearch/elasticsearch-analysis-voikko/0.2.0
