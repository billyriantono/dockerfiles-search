FROM maven:3.5.0-jdk-8-alpine

# ###################################
# Image core configuration
# ###################################
# Configure image arguments
ARG SPRING_APPLICATION_NAME
# Assign arguments to environment
ENV SPRING_APPLICATION_NAME=$SPRING_APPLICATION_NAME
# Configure service workspace folder
RUN mkdir -p workspace/sys-stack-serv-config
# Add service files
ADD . /workspace/sys-stack-serv-config

# ###################################
# Install 3rd party dependencies
# ###################################
# Install JCE
WORKDIR /workspace/sys-stack-serv-config/src/main/resources/vendor/oracle/JCE/
RUN unzip UnlimitedJCEPolicyJDK7.zip && \
	cp /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/local_policy.jar /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/local_policy.jar.bak && \
	cp /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/US_export_policy.jar /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/US_export_policy.jar.bak && \
	cp UnlimitedJCEPolicy/local_policy.jar /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/local_policy.jar && \
	cp UnlimitedJCEPolicy/US_export_policy.jar /usr/lib/jvm/java-1.8-openjdk/jre/lib/security/US_export_policy.jar && \
	rm -rf UnlimitedJCEPolicy

# ###################################
# Package build
# ###################################
# Build source code using Maven with dev profile/arguments
WORKDIR /workspace/sys-stack-serv-config
RUN mvn \
    -DSPRING_APPLICATION_NAME=config \
    clean package install

# ###################################
# Declare image ports and entry-points
# ###################################
# Expose service port
EXPOSE 9999
# Define image entry-points
RUN ["chmod", "+x", "./docker-entrypoint.sh"]
ENTRYPOINT [ "/bin/bash", "-l", "./docker-entrypoint.sh" ]
