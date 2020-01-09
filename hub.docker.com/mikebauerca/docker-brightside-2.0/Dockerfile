# This Dockerfile is used to build an image capable of running brightside 2.0 commands
FROM ahumanfromca/jenkins-npm-agent

# Sets the scoped registry for brightside packages
USER jenkins
RUN npm config set @brightside:registry https://api.bintray.com/npm/ca/brightside

# Installs brightside
RUN npm install -g @brightside/core@2.0.0-next.201812071333

USER root
