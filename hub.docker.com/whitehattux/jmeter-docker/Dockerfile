FROM openjdk:8-alpine

LABEL maintainer="David Sperling <dsperling@smithmicro.com>"

ENV JMETER_VERSION apache-jmeter-5.0
ENV JMETER_HOME /opt/$JMETER_VERSION
ENV PATH $PATH:$JMETER_HOME/bin
ENV CMDRUNNER_VERSION 2.2
ENV PLUGINMGR_VERSION 1.3

# overridable environment variables
ENV RESULTS_LOG results.jtl

# Install the required tools for JMeter
RUN apk add --update --no-cache \
    curl \
    openssh-client

WORKDIR /opt

# install JMeter and the JMeter Plugins Manager
RUN curl -O https://archive.apache.org/dist/jmeter/binaries/$JMETER_VERSION.tgz \
  && tar -xvf $JMETER_VERSION.tgz \
  && rm $JMETER_VERSION.tgz \
  && rm -rf $JMETER_VERSION/docs $JMETER_VERSION/printable_docs \
  && cd $JMETER_HOME/lib \
  && curl -O http://search.maven.org/remotecontent?filepath=kg/apc/cmdrunner/$CMDRUNNER_VERSION/cmdrunner-$CMDRUNNER_VERSION.jar \
  && cd $JMETER_HOME/lib/ext \
  && curl -O http://search.maven.org/remotecontent?filepath=kg/apc/jmeter-plugins-manager/$PLUGINMGR_VERSION/jmeter-plugins-manager-$PLUGINMGR_VERSION.jar \
  && java -cp jmeter-plugins-manager-$PLUGINMGR_VERSION.jar org.jmeterplugins.repository.PluginManagerCMDInstaller

# install all available plugins except for those that are deprecated
#RUN PluginsManagerCMD.sh install-all-except jpgc-hadoop,jpgc-oauth \
#  && sleep 2 \
#  && PluginsManagerCMD.sh status

ADD https://github.com/WhiteHatTux/JmeterSockJsSampler/releases/download/v0.0.1/org-mi-jmeter-sockjssampler-0.0.1-SNAPSHOT.jar /opt/$JMETER_VERSION/lib/ext/

# copy our entrypoint
COPY entrypoint.sh /opt/jmeter/

WORKDIR /logs

EXPOSE 1099 50000 51000 4445/udp

# default command in the entrypoint is 'minion'
ENTRYPOINT ["/opt/jmeter/entrypoint.sh"]