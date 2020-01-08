###
# Information and Instructions
###
# Dockerfile for the creating Jenkins master, starts out of the box with no configuration.C
# admin user based on Docker secrets. See the attached readme file.
# Extends: jenkins/jenkins:2.78-alpine
# Installs the following software:
# None
###
## To build:
# docker build -t jenkins-master:latest .
## To run interactive:
# docker run -it -p 8080:8080 -p 50000:50000 --network ci-network --name jenkins-master jenkins-master:latest
# To run as a service in swarm mode (use --with-registry-auth if from a private registry)
# docker service create --network ci-network --secret jenkins-user --secret jenkins-pass --name jenkins -p 8080:8080 -p 50000:50000 mononoke/jenkins-master:latest
## To run in background:
# docker run -d --name jenkins-master jenkins-master:latest
## To login when running
# docker exec -i -t (containerId) bash # obtain the containerId from docker ps
## to tag for pushing, e.g.
# docker tag jenkins-master:latest mononoke/jenkins-master:1.0.1
## to push
# docker push mononoke/jenkins-master:1.0.1
## to pull
# docker pull mononoke/jenkins-master:1.0.1
################################################
# Some useful Docker commands
# To list running docker containers: "docker ps"
# When running in the background, the container needs to be stopped.
#  - type "docker ps" to get the container id
#  - type "docker stop {containerid}"
#  - type "docker rm {id}
# To log in to the container: "docker exec -it {containerid} bash"
# login to ecr aws ecr get-login --no-include-email --region ap-northeast-1 | sh
# docker service update --with-registry-auth  --image mononoke/jenkins-master:1.0.1 jenkins
# --env JAVA_OPTS=-Dhudson.footerURL=http://mycompany.com
###############################################

FROM jenkins/jenkins:2.78-alpine

ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

### Copy over the various groovy scripts to make set up less manual
COPY security.groovy /usr/share/jenkins/ref/init.groovy.d/security.groovy

COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/executors.groovy

COPY sonar-runner.groovy /usr/share/jenkins/ref/init.groovy.d/sonar-runner.groovy

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt

## if wanted, better to leave the option to run time
#ENV JENKINS_OPTS --prefix=/jenkins

RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt