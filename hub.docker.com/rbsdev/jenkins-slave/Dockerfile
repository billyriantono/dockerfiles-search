FROM java:8-jre-alpine

ENV JENKINS_URL=''
ENV JENKINS_SECRET=''
ENV JENKINS_NODE_NAME=''

RUN sed -i -e 's/v3\.4/v3.6/g' /etc/apk/repositories

RUN apk add --no-cache git docker curl

RUN git config --global http.sslVerify false

RUN mkdir -p /etc/jenkins

CMD curl -o /etc/jenkins/slave.jar $JENKINS_URL/jnlpJars/slave.jar && \
   java -jar /etc/jenkins/slave.jar -jnlpUrl $JENKINS_URL/computer/$JENKINS_NODE_NAME/slave-agent.jnlp -secret $JENKINS_SECRET