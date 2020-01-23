FROM docker:17.05.0-ce-git
LABEL maintainer="Antoine Boisadam (GH: Antoine38660)"

#Install OpenJDK
RUN apk add --no-cache \
		openjdk8 \
		maven
#Set Java home 
ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
