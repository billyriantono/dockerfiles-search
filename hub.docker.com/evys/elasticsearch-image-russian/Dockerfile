FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.9

WORKDIR /usr/share/elasticsearch

RUN bin/elasticsearch-plugin install http://dl.bintray.com/content/imotov/elasticsearch-plugins/org/elasticsearch/elasticsearch-analysis-morphology/5.6.9/elasticsearch-analysis-morphology-5.6.9.zip
RUN bin/elasticsearch-plugin remove x-pack
