FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.9

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin remove x-pack && \
	/usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu
