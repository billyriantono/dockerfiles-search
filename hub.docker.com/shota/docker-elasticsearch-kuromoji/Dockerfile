FROM docker.elastic.co/elasticsearch/elasticsearch:6.2.4

LABEL maintainer "koharashota <transparent.blue69@gmail.com>"

# Plugin x-pack already exists in this image
# RUN elasticsearch-plugin install --batch x-pack
RUN elasticsearch-plugin install analysis-kuromoji

