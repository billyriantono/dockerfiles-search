# Use alpine as base image
FROM alpine:latest

# Set maintainer info
MAINTAINER Miguel Luis <mkxpto@gmail.com>

# Set environment variables
ENV JAVA_ALPINE_VERSION 8.131.11-r2

ENV CRAFTBUKKIT craftbukkit-1.8.8-R0.1-SNAPSHOT-latest.jar

# Install dependencies
RUN apk --update add --no-cache openjdk8-jre="$JAVA_ALPINE_VERSION" ca-certificates wget && \
	update-ca-certificates && \
	wget -q https://cdn.getbukkit.org/craftbukkit/$CRAFTBUKKIT

# Set working directory
WORKDIR /data

# Define volumes
VOLUME /data

# Set exposed port
EXPOSE 25565

# Run
CMD echo eula=true > /data/eula.txt && java -jar /$CRAFTBUKKIT
