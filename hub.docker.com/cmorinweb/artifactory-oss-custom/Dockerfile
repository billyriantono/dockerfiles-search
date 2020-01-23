FROM docker.bintray.io/jfrog/artifactory-oss:latest

LABEL maintainer "charles.morin@cra-arc.gc.ca"

COPY entrypoint-artifactory-oss-custom.sh /home/jfrog-artifactory-oss/bin/entrypoint-artifactory-oss-custom.sh
COPY artifactory.config.xml /home/jfrog-artifactory-oss/config/artifactory.config.xml
COPY postgresql-42.2.5.jar /home/jfrog-artifactory-oss/driver/postgresql-42.2.5.jar

# We are using the copy approach since we have Artifactory OSS. 
# JFrog CLI and REST APIs are available only starting from the Pro version of Artifactory.
# With Artifactory Pro, we will be able to use JFrog CLI to add the desired configurations, which will make use of Artifactory's REST API under the hood.
# 
ENTRYPOINT ["/bin/bash", "-c", "/home/jfrog-artifactory-oss/bin/entrypoint-artifactory-oss-custom.sh"]

# Artifactory OSS doesn't allow changing password from JFrog CLI or directly from the REST API.
# Artifactory Pro is required to achieve that requirement.
# RUN curl -X POST -u admin:password -H "Content-type: application/json" -d '{ "userName" : "admin", "oldPassword" : "password", "newPassword1" : "THE NEW PASSWORD", "newPassword2" : "THE NEW PASSWORD (AGAIN)" }' http://artifactory-server:8081/artifactory/api/security/users/authorization/changePassword
