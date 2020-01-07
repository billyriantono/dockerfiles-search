FROM strm/task:latest

MAINTAINER opsxcq <opsxcq@thestorm.com.br>

VOLUME /data
WORKDIR /data

COPY gdrivelinux_amd64 /bin/gdrive
COPY main.sh /
ENTRYPOINT ["/main.sh"]
CMD ["default"]

