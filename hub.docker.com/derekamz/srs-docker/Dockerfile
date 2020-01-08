FROM centos:latest
COPY srs /srs
COPY entrypoint.sh /entrypoint.sh
VOLUME /data

EXPOSE 1935 1985
ENTRYPOINT ["/entrypoint.sh"]
