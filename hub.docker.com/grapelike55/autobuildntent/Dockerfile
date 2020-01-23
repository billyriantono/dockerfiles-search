FROM docker.elastic.co/elasticsearch/elasticsearch:6.5.4

# プラグインのインストール
RUN bin/elasticsearch-plugin install analysis-kuromoji && \
	bin/elasticsearch-plugin install analysis-icu && \
	bin/elasticsearch-plugin install repository-s3 --batch && \
	bin/elasticsearch-plugin install repository-gcs --batch
