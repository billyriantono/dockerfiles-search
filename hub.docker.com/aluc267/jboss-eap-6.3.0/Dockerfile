# Steps taken to create this image
# docker build --rm -t jboss/jboss_eap:6.3.0  .
# docker run -p 9990:9990 -p 9999:9999 -p 8080:8080 -it jboss/jboss_eap:6.3.0
# 
# Get required ZIP file from: https://access.redhat.com/jbossnetwork/restricted/softwareDownload.html?softwareId=32483&product=appplatform

FROM jboss/base-jdk:7
ADD jboss /opt/jboss/jboss-eap-6.3
USER root

# Add EAP_HOME environment variable, to easily upgrade the script for different EAP versions
ENV EAP_HOME /opt/jboss/jboss-eap-6.3
ENV JBOSS_HOME /opt/jboss/jboss-eap-6.3
WORKDIR /opt/jboss/jboss-eap-6.3

RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

ENTRYPOINT ["/opt/jboss/jboss-eap-6.3/bin/standalone.sh"]
CMD []
