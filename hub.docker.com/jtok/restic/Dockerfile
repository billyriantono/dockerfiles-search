### Dockerfile for restic
### Originally from Lobaro/restic-backup-docker
FROM phusion/baseimage:0.10.0
LABEL maintainer="jtok"


ENV RESTIC_VERSION=0.8.3
ENV RESTIC_FILE_NAME=restic_${RESTIC_VERSION}_linux_amd64


#RUN apk update && apk add ca-certificates

#FROM busybox:glibc

#COPY --from=certs /etc/ssl/certs /etc/ssl/certs

# Configure user nobody to match unRAID's settings
RUN usermod -u 99 nobody && \
    usermod -g 100 nobody && \
    usermod -d /home nobody && \
    chown -R nobody:users /home


# Install tzdata and set timezone environment variable
RUN apt update && apt install -y tzdata \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV TZ=America/Chicago

# Enable sshd for remote management
RUN rm -f /etc/service/sshd/down

# Regenerate SSH host keys. baseimage-docker does not contain any, so you
# have to do that yourself. You may also comment out this instruction; the
# init system will auto-generate one during boot.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Get restic executable
ADD https://github.com/restic/restic/releases/download/v${RESTIC_VERSION}/${RESTIC_FILE_NAME}.bz2 /
RUN apt-get update -q \
  && apt-get install -y --no-install-recommends bzip2 \
  && bzip2 -d ${RESTIC_FILE_NAME}.bz2 \
  && mv ${RESTIC_FILE_NAME} /bin/restic \
  && chmod +x /bin/restic


#RUN mkdir -p /mnt/restic /var/spool/cron/crontabs /var/log
RUN mkdir -p /mnt/restic /sshkey \
  && chown -R nobody:users /mnt/restic

ENV RESTIC_REPOSITORY=/mnt/restic
ENV RESTIC_PASSWORD=""
ENV RESTIC_TAG=""
ENV NFS_TARGET=""
# By default backup every day at 06:00 hours
ENV BACKUP_CRON="0 6 * * *"
ENV RESTIC_FORGET_ARGS=""
ENV RESTIC_JOB_ARGS=""

ENV B2_ACCOUNT_ID=""
ENV B2_ACCOUNT_KEY=""


# Set up port for ssh
EXPOSE 22/tcp

# /mnt/restic is for your a local restic repository
# /data is the dir where you have to put the data to be backed up
# /sshkey is where you will upload your ssh public key so that it becomes the authorized key when your container boots
### IMPORTANT: They container will need your public key to stay in that directory if you want it persistent. It must be named sshkey.pub.
### I suggest using a unique key pair that's only for talking to this container.
VOLUME ["/mnt/restic", "/data", "/sshkey"]

COPY backup.sh /bin/backup
RUN chmod +x /bin/backup
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

#create blank sshkey.pub
RUN touch /sshkey/sshkey.pub
#RUN touch /var/log/cron.log

WORKDIR /

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/sbin/my_init"]

### END
