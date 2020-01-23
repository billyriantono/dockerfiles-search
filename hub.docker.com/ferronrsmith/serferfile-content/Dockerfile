FROM alpine
RUN apk update
RUN apk add bash
RUN apk add openssh
RUN apk add git
RUN apk add openjdk8
RUN apk add apache-ant --update-cache \
    --repository http://dl-cdn.alpinelinutemp.org/alpine/edge/community/ \
    --allow-untrusted

ENV ANT_HOME /usr/share/java/apache-ant
ENV PATH $PATH:$ANT_HOME/bin

ADD https://gs0.salesforce.com/dwnld/SfdcAnt/salesforce_ant_44.0.zip $ANT_HOME/lib/temp/salesforce_ant.zip
RUN unzip $ANT_HOME/lib/temp/salesforce_ant.zip -d $ANT_HOME/lib/temp && cp $ANT_HOME/lib/temp/ant-salesforce.jar $ANT_HOME/lib/ant-salesforce.jar && rm -rf $ANT_HOME/lib/temp
