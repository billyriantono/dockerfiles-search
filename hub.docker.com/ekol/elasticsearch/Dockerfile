# Dockerfile
FROM elasticsearch:2.4.6
ADD plugins/analysis-icu-2.4.6.zip /usr/share/elasticsearch/plugins/analysis-icu-2.4.6.zip
RUN sh -c 'unzip /usr/share/elasticsearch/plugins/analysis-icu-2.4.6.zip -d /usr/share/elasticsearch/plugins/analysis-icu/'
RUN sh -c 'rm -rf /usr/share/elasticsearch/plugins/analysis-icu-2.4.6.zip'
ADD docker-entrypoint.sh /
