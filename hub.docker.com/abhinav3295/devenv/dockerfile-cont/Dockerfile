FROM debian:latest

LABEL mantainer="Gius. Camerlingo <gcamerli@gmail.com>"
LABEL version="1.0"
LABEL description="Backup storage to AWS S3 for Docker."

# Docker image name
ENV NAME=backup

# Update system and install packages
RUN apt-get update 
RUN apt-get install -y --no-install-recommends \
	curl \
	cron 
RUN apt-get install -y python-pip
RUN pip install awscli

# Clean system
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Copy scripts
COPY /scripts /dockup/
RUN chmod 755 /dockup/*.sh

# AWS variables to be overwritten
ENV S3_BUCKET_NAME docker-backups.example.com
ENV AWS_ACCESS_KEY_ID **DefineMe**
ENV AWS_SECRET_ACCESS_KEY **DefineMe**
ENV AWS_DEFAULT_REGION us-east-1
ENV PATHS_TO_BACKUP auto
ENV BACKUP_NAME backup
ENV RESTORE false
ENV RESTORE_TAR_OPTION --preserve-permissions
ENV NOTIFY_BACKUP_SUCCESS false
ENV NOTIFY_BACKUP_FAILURE false
ENV BACKUP_TAR_TRIES 5
ENV BACKUP_TAR_RETRY_SLEEP 30

# Timezone
ENV TZ="Europe/Paris"

# User
RUN useradd -ms /bin/bash docker

# Home
ENV HOME=/home/docker

# Permissions
RUN chown -R docker:docker $HOME

# Healthcheck
COPY healthcheck /usr/local/bin/
RUN chmod 744 /usr/local/bin/healthcheck

# Change user
USER docker

# Entrypoint
WORKDIR /dockup
CMD ["./run.sh"]
