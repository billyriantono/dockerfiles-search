FROM alpine:latest

RUN sed -i -e "s/#//" /etc/apk/repositories && \
	apk update && \
	apk add --no-cache ffmpeg jq

COPY ./input.conf /etc/timelapse-recorder/input.conf
COPY ./timelapse-recorder /bin/timelapse-recorder
WORKDIR /mnt/storage

RUN chmod +x /bin/timelapse-recorder

CMD ["timelapse-recorder"]
