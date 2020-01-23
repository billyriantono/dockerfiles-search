FROM debian:stretch-slim

COPY oracle-java8-jre_8u221_amd64.deb /tmp

RUN set -x && \
	cd /tmp && \
	mkdir -p /usr/share/man/man1 && \
	apt update && apt --fix-broken install -y ./oracle-java8-jre_8u221_amd64.deb && \
	apt install -y wget && \
	java -version && \
	apt purge -y --auto-remove wget


COPY vaccine-0.0.1.jar /data/program.jar

ENTRYPOINT ["java","-jar","/data/program.jar"]
