FROM tomcat:8-jre8

LABEL  maintainer "tani_k <kazuki@higashitani.org>"

ENV GITBUCKET_HOME /var/gitbucket

RUN rm -rf /usr/local/tomcat/webapps/ROOT

ADD https://github.com/gitbucket/gitbucket/releases/download/4.23.0/gitbucket.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080 29418

CMD [ "/usr/local/tomcat/bin/catalina.sh", "run" ]
