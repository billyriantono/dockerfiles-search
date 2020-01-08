FROM alpine:3.8
RUN apk update
RUN apk add --no-cache py-pip py-magic mongodb-tools && pip install s3cmd --upgrade pip
ADD entrypoint.sh /root/entrypoint.sh
ADD backup.sh /root/backup.sh
ENTRYPOINT ["/root/entrypoint.sh"]
CMD [ "crond", "-f" ]