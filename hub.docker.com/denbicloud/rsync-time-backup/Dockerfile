FROM oxys/alpine-docker-cron:latest

RUN apk update && apk add rsync openssh bash
ADD rsync_tmbackup.sh /rsync_tmbackup.sh
