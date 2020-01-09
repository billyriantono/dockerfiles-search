FROM alpine
MAINTAINER kongroo <imjcqt@gmail.com>

# example: docker run --rm -v /path/to/save/:/root kongroo/aria2 http://xxx.com/xxx.txt

COPY aria2.conf /etc/aria2/
RUN set -xe \
&& apk add -U aria2 \
&& rm -rf /var/cache/apk/* 

ENTRYPOINT ["aria2c", "--conf-path=/etc/aria2/aria2.conf"]
CMD ["--help"]
EXPOSE 6800
