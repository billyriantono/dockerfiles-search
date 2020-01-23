FROM  centos:7
MAINTAINER Peter Wu <piterwu@outlook.com>
ENV LANG=C.UTF-8 \
    MAILSERVER='' \
    MAIL_PORT='25' \
    MAIL_USER='' \
    MAIL_PASSWORD='' \
    MAIL_NAME='禅道'

COPY ZenTaoPMS.zbox_64.tar.gz /opt
ADD /entrypoint.sh /
RUN chmod +x /entrypoint.sh && \
    groupadd -g 1000 zentao && \
    useradd -u 1000 -g zentao zentao

VOLUME ["/opt/zbox/data"]
EXPOSE 80

CMD ["/entrypoint.sh"]