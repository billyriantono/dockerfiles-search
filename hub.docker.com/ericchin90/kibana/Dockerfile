# VERSION			0.0.1
# BUILD-USING:		docker build -t ericchin90/elasticsearch .
# PUSH-USING:		docker push ericchin90/elasticsearch

FROM		httpd
MAINTAINER 	Eric Chin <ericchin90@gmail.com>

RUN apt-get update && apt-get -y install wget

WORKDIR /usr/local/apache2/htdocs

RUN wget -q -O kibana.tar.gz https://download.elasticsearch.org/kibana/kibana/kibana-3.1.2.tar.gz \
	&& tar -zxf kibana.tar.gz \
	&& rm kibana.tar.gz \
	&& mv kibana-3.1.2/* . \
	&& rm -rf kibana-3.1.2

# RUN sed -i '/window.location.hostname/c\    elasticsearch: "http://elasticsearch:9200,"' config.js