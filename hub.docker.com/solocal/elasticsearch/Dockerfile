FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.8.4

RUN elasticsearch-plugin install --batch discovery-ec2 \
 && elasticsearch-plugin install --batch repository-s3
