FROM schickling/s3cmd

COPY s3cfg /root/.s3cfg

COPY docker-entrypoint.sh /usr/local/bin/

ENTRYPOINT ["sh", "/usr/local/bin/docker-entrypoint.sh"]
