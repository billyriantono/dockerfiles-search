FROM mysql:8

MAINTAINER Ioannis Angelakopoulos<ioagel@gmail.com>

# just install bzip2 for better compression in mysql backups
RUN apt-get update && apt-get install -y --no-install-recommends bzip2 && rm -rf /var/lib/apt/lists/*

COPY mysql-backup.sh .
RUN chmod +x mysql-backup.sh

CMD ["./mysql-backup.sh"]
