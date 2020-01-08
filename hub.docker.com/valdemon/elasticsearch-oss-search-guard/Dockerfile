ARG COMPAT=6.6.1
FROM docker.elastic.co/elasticsearch/elasticsearch-oss:$COMPAT

ARG VERSION=6.6.1-24.1

RUN bin/elasticsearch-plugin install -b https://search.maven.org/classic/remotecontent?filepath=com/floragunn/search-guard-6/$VERSION/search-guard-6-$VERSION.zip
