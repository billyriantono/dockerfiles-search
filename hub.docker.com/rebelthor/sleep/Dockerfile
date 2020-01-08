FROM alpine:latest
RUN apk update && apk upgrade && apk add bash curl python3 && rm -rf /var/cache/*/*
RUN pip3 install --upgrade pip setuptools httpie && rm -r /root/.cache
ADD sleep.sh /
RUN chmod +x sleep.sh
ENTRYPOINT [ "/sleep.sh" ]