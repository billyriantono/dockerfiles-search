FROM ubuntu:16.04
MAINTAINER volnet <volnet@tom.com>
ENV REFRESHED_AT 2017-06-26

RUN apt-get update && apt-get install -y --no-install-recommends \
	curl \
	default-jre && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir jenkins && cd jenkins \
	&& curl -O -L "http://mirrors.jenkins.io/war-stable/latest/jenkins.war"

EXPOSE 8080

WORKDIR "jenkins/"

CMD ["java", "-jar", "jenkins.war"]
