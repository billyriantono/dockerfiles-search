FROM aidbox/db:passive-latest

ADD docker-entrypoint.sh .
ADD make-backup.sh .
ADD export-backup.sh .

ENTRYPOINT ["./docker-entrypoint.sh"]
