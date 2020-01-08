FROM java:8-jre
ENV IMPORTER_VERSION 1.7.3.0
RUN wget -c -t 5 http://xbib.org/repository/org/xbib/elasticsearch/importer/elasticsearch-jdbc/${IMPORTER_VERSION}/elasticsearch-jdbc-${IMPORTER_VERSION}-dist.zip && \
	unzip elasticsearch-jdbc-${IMPORTER_VERSION}-dist.zip && \
	rm ./elasticsearch-jdbc-${IMPORTER_VERSION}-dist.zip && \
	mv ./elasticsearch-jdbc-${IMPORTER_VERSION} /usr/local
ENV PATH /usr/local/elasticsearch-jdbc-${IMPORTER_VERSION}/bin:$PATH

COPY ./docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD []
