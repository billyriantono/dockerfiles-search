FROM mongo:3.4.10-jessie
MAINTAINER alex-saf

# Install backup script
COPY moose-mongo-backup.sh /app/
RUN chmod -R 755 /app/moose-mongo-backup.sh

WORKDIR /app

#ENTRYPOINT ["/bin/bash", "-e", "/app/moose-mongo-backup.sh"]

CMD ["/app/moose-mongo-backup.sh"]
