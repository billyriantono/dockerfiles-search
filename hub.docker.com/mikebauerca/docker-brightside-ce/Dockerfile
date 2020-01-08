# This Dockerfile is used to build an image capable of running brightside 2.0 commands
FROM ahumanfromca/jenkins-npm-agent

# Sets the scoped registry for brightside packages
USER jenkins
RUN npm config set @brightside:registry https://api.bintray.com/npm/ca/brightside

# Installs brightside
RUN npm install -g @brightside/core@next

RUN bright plugins install @brightside/endevor@next
RUN bright plugins install @brightside/filemasterplus@next
RUN bright plugins install @brightside/ops@next

RUN bright plugins install @brightside/cics@next
RUN bright plugins install @brightside/db2@next

USER root
