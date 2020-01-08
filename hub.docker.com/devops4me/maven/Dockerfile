
# --->
# ---> Going with the Long Term Support version
# ---> of Maven.
# --->
FROM maven:3.6.0-jdk-11
USER root

# --->
# ---> Insert the maven settings that defines a localhost Nexus
# ---> repository and the credentials necessary to write to it
# --->

COPY settings.xml /root/.m2/settings.xml

# --->
# ---> When running this image map the codebase to
# ---> this directory location.
# --->
RUN mkdir -p /root/codebase
WORKDIR /root/codebase
