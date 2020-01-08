FROM gcr.io/cloudsql-docker/gce-proxy:1.12

ENV CLOUD_SQL_INSTANCE_CONNECTION project-id:region:database-name

copy start.sh /start.sh

CMD ["/start.sh"]