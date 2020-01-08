FROM docker.elastic.co/elasticsearch/elasticsearch:5.5.3

RUN elasticsearch-plugin remove x-pack
RUN elasticsearch-plugin install discovery-ec2
