FROM alpine:3.7

ADD export.sh /root/
ADD export-file.sh /root/

RUN echo '*  *  *  *  * /root/export.sh' > /etc/crontabs/root
CMD ["crond", "-l", "2", "-f"]

