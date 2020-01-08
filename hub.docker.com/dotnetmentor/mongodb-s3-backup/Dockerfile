FROM mongo:4.1.10-bionic
RUN apt-get update && apt-get install -y awscli && aws --version
RUN apt-get update && apt-get install -y curl
COPY ./backup-to-s3 /usr/bin/
ENTRYPOINT "/usr/bin/backup-to-s3"
