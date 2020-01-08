FROM openjdk:jre-alpine

RUN apk update \
	&& apk add ttf-dejavu \
	&& wget -q http://umlet.com/umlet_14_3/umlet-standalone-14.3.0.zip \
	&& unzip -q umlet-standalone-14.3.0.zip 

WORKDIR "/Umlet"

CMD ["java", "-jar", "umlet.jar", "-action=convert"]
