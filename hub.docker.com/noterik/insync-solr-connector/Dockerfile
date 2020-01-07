FROM python:3.6.5-alpine
RUN apk update && apk add --no-cache curl mongodb
RUN pip install --no-cache-dir 'mongo-connector[solr]'
ADD . /opt/insync-solr-connector
RUN chmod +x /opt/insync-solr-connector/start.sh
RUN touch mongo-connector.log
CMD /opt/insync-solr-connector/start.sh && tail -f /var/log/mongo-connector.log
