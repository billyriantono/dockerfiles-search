FROM alpine:3.8

RUN apk add --update --no-cache openssh sshpass bash lftp gettext

RUN echo 'set sftp:connect-program "ssh -a -x -i ~/.ssh/pipelines_id"' >> /etc/lftp.conf

COPY batch_default /etc/pipe/
COPY pipe.sh /usr/bin/
ENTRYPOINT ["pipe.sh"]
