FROM opensourcefoundries/alpine:edge

RUN apk add --no-cache git openjdk8-jre-base ca-certificates shadow curl runit

RUN mkdir /opt \
    && cd opt/ \
	&& git clone https://github.com/badboy-huaqiao/simple-local-gateway-console console

RUN useradd -r -d /opt/console -s /sbin/nologin -U console-user

CMD cd /opt/console/docker-files \
    && chpst -u console-user java -jar -Dspring.config.location=./application.properties simple-local-gateway-console.jar
