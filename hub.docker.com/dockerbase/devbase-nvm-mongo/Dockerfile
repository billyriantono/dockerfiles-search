# VERSION 1.2
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Devbase-nvm-mongo Image Container

FROM dockerbase/devbase-nvm

USER    root
# Run dockerbase script
ADD     devbase-nvm-mongo.sh /dockerbase/
RUN     /dockerbase/devbase-nvm-mongo.sh

ADD     java.sh /dockerbase/
RUN     /dockerbase/java.sh

ENV     JAVA_HOME /usr/local/java
ENV     JRE_HOME /usr/local/java/jre
ENV     PATH $PATH:$JAVA_HOME/bin:$JRE_HOME/bin

USER    devbase
