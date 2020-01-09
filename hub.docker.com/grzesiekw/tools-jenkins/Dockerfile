FROM jenkins

MAINTAINER grzesiekw "g.wilkowicz@gmail.com"

ADD jenkins_home /var/jenkins_home
ADD jenkins /var/lib/jenkins

USER root

RUN chown -R jenkins /var/jenkins_home && chown -R jenkins /var/lib/jenkins

USER jenkins

CMD java -jar /usr/share/jenkins/jenkins.war $JENKINS_ARGS
