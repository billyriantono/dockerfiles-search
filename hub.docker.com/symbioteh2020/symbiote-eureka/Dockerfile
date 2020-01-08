FROM openjdk:8-jre-alpine

WORKDIR /home

ENV componentName "EurekaService"
ENV componentVersion 3.0.2

RUN apk --no-cache add \
	git \
	unzip \
	wget \
	bash \
        && echo "Downloading $componentName $componentVersion" \
	&& wget "https://jitpack.io/com/github/symbiote-h2020/$componentName/$componentVersion/$componentName-$componentVersion-run.jar"

EXPOSE 8761

CMD java $JAVA_HTTP_PROXY $JAVA_HTTPS_PROXY $JAVA_NON_PROXY_HOSTS -jar $(ls *run.jar)
