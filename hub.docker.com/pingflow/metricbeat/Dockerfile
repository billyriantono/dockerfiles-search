FROM docker.elastic.co/beats/metricbeat:6.2.1

ENV ES_HOSTS 'elasticsearch:9200'
ENV ES_PROTO 'http'
ENV ES_USER 'elastic'
ENV ES_PASS 'changeme'
ENV ES_BULK_SIZE_MAX 2

ENV KB_HOST 'kibana:5601'

ENV MB_APACHE_ENABLE false
ENV MB_DOCKER_ENABLE false
ENV MB_KUBERNETES_ENABLE false
ENV MB_MYSQL_ENABLE false
ENV MB_NGINX_ENABLE false
ENV MB_REDIS_ENABLE false
ENV MB_SYSTEM_ENABLE false

COPY entrypoint.sh /usr/local/bin/entrypoint

ENTRYPOINT ["entrypoint"]
CMD ["run"]
