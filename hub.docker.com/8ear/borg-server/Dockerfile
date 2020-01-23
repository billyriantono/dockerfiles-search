FROM alpine
Maintainer 8ear

ENV BORG_VERSION=1.1.5

RUN apk add --no-cache \
    openssl-dev \
    python3-dev \
    musl-dev \
    gcc \
    acl-dev \
    linux-headers \
    lz4-dev \
    sshfs

# Upgrade PIP3
RUN pip3 install --upgrade pip

# Add BORG User
RUN adduser -u 500 -D -g "Borg Backup" borg \ 
     && mkdir -p /borg/repo \ 
     && chown -R borg.borg /borg \ 
     && mkdir /home/borg/.ssh \ 
     && chmod 700 /home/borg/.ssh \ 
     && chown borg.borg /home/borg/.ssh

# Install Borgbackup tools
RUN pip3 install borgbackup==$BORG_VERSION

# Setup LANGUAGE
ENV LANG en_US.UTF-8

# Copy init script
# COPY borg-backup.sh /
# RUN chmod +x /borg-backup.sh

VOLUME /borg
EXPOSE 23 

ENTRYPOINT [ "borg" ]