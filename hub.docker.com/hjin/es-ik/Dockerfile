FROM elasticsearch:6.7.0
VOLUME /usr/share/elasticsearch/data
RUN ["./bin/elasticsearch-plugin", "install", "--batch", "https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.7.0/elasticsearch-analysis-ik-6.7.0.zip"]
