FROM centos
MAINTAINER Farhan Sajid <farhansajid7861@gmail.com>

USER root
# Installing node.js
RUN yum -y install epel-release &&\
    yum -y install nodejs


# Copy testing to /app
# Copy this entire directory except .gitignore files
COPY . /app
WORKDIR /app


# Installing application dependencies
RUN npm install -g mocha &&\
    npm install -g mocha-jenkins-reporter &&\
    npm install

# Set entrypoint to run mocha test runner
ENTRYPOINT ["mocha"]
