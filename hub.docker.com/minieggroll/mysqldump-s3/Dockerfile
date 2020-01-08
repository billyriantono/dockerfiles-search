FROM alpine:latest

RUN mkdir -p /aws && \
	apk -Uuv add groff less python py-pip mysql-client && \
	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/*

ENV AWS_ACCESS_KEY_ID **None**
ENV AWS_SECRET_ACCESS_KEY **None**
ENV AWS_BUCKET **None**

ADD dump /dump
RUN chmod +x /dump

CMD ["sh", "/dump"]
