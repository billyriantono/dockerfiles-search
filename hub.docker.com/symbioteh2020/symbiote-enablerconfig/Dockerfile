FROM openjdk:8-jre-alpine

WORKDIR /home

ENV componentName "EnablerConfigService"
ENV componentVersion 2.2.0

RUN apk --no-cache add \
	git \
	unzip \
	wget \
	bash \
	&& echo "Downloading $componentName $componentVersion" \
	&& wget "https://jitpack.io/com/github/symbiote-h2020/$componentName/$componentVersion/$componentName-$componentVersion-run.jar" \
	&& touch bootstrap.properties \
	&& echo "spring.cloud.config.server.git.uri=file://$PWD/EnablerConfigProperties" >> bootstrap.properties \
	&& echo "server.port=8888" >> bootstrap.properties


EXPOSE 8888

CMD java $JAVA_HTTP_PROXY $JAVA_HTTPS_PROXY $JAVA_NON_PROXY_HOSTS -jar $(ls *run.jar)