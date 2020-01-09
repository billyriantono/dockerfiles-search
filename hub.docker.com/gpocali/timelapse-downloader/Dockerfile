FROM alpine:latest

RUN sed -i -e "s/#//" /etc/apk/repositories && \
	apk update && \
	apk add --no-cache jq tzdata

COPY ./input.conf /etc/timelapse-downloader/input.conf
COPY ./timelapse-downloader /bin/timelapse-downloader
COPY ./deleteEarliestFile /bin/deleteEarliestFile
WORKDIR /mnt/storage

RUN chmod +x /bin/timelapse-downloader

CMD ["timelapse-downloader"]
