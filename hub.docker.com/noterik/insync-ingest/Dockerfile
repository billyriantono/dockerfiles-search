 # Alpine with java and cron

FROM alpine:latest as builder

# Install dependencies
RUN apk update && \
	apk upgrade && \
	apk add bash maven openjdk8

COPY . /opt/app
RUN mkdir /opt/app/dist

WORKDIR /opt/app

RUN chmod 0755 build.sh && ./build.sh

FROM alpine:latest

RUN apk update && \
	apk upgrade && \
	apk add  --no-cache bash openjdk8

RUN mkdir -p /opt/app/docker
RUN mkdir -p /opt/app/dist

ADD ./docker /opt/app/docker
COPY ./docker/ingest-config.xml /opt/app
COPY --from=builder /opt/app/dist /opt/app/dist

VOLUME /media/insync

RUN touch /var/log/cron.log

# Give execution rights on the cron job
RUN chmod 0755 /opt/app/docker/do-ingest.sh

# Add to crontab
RUN echo '*  *  *  *  *    /opt/app/docker/do-ingest.sh' > /etc/crontabs/root

CMD ["/usr/sbin/crond", "-f", "-d", "0", "&&", "tail", "-f", "/var/log/cron.log"]
