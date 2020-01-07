FROM elasticsearch:5.1

COPY config/elastic.yml /elasticsearch/config/elasticsearch.yml

# Install Elasticsearch plug-ins
RUN bin/elasticsearch-plugin install discovery-ec2

# Set environment
ENV AWS_KEY key
ENV AWS_SECRET secret

ENV TAG_KEY somekey
ENV TAG_VALUE somevalue