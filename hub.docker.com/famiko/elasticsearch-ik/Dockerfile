FROM elasticsearch:2.4.4

ENV IK_VERSION 1.10.4

ADD https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${IK_VERSION}/elasticsearch-analysis-ik-${IK_VERSION}.zip /tmp/elasticsearch-analysis-ik.zip

RUN mkdir /usr/share/elasticsearch/plugins/ik && \
  unzip /tmp/elasticsearch-analysis-ik.zip -d /usr/share/elasticsearch/plugins/ik 

EXPOSE 9200 9300

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
