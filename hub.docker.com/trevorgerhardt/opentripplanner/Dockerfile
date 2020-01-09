
#
# OpenTripPlanner Dockerfile
#
# https://github.com/opentripplanner/opentripplanner
#

# Start with a small Ubuntu base image
FROM ubuntu:14.04

# Install java
RUN \
  apt-get update && \
  apt-get install -y openjdk-7-jre wget && \
  rm -rf /var/lib/apt/lists/*

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

# Add latest jar.
RUN mkdir -p /var/otp/graphs && wget -q -O /var/otp/otp.jar http://dev.opentripplanner.org/jars/otp-latest-master.jar

# Expose ports for other containers
EXPOSE 8080
EXPOSE 8081

ENTRYPOINT [ "java", "-Xmx6G", "-Xverify:none", "-jar", "/var/otp/otp.jar" ]

CMD [ "--help" ]
