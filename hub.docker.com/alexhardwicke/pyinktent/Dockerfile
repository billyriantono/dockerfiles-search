FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.8

WORKDIR /usr/share/elasticsearch
RUN bin/elasticsearch-plugin install http://dl.bintray.com/content/imotov/elasticsearch-plugins/org/elasticsearch/elasticsearch-analysis-morphology/5.6.8/elasticsearch-analysis-morphology-5.6.8.zip
RUN bin/elasticsearch-plugin install repository-s3
