FROM alpine
MAINTAINER rob@robtimmer.com

EXPOSE 25565
VOLUME ["/data"]

RUN apk add openjdk8-jre-base --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted \
    && rm -rf /var/cache/apk/*
	
ENTRYPOINT ["./data/start.sh"]