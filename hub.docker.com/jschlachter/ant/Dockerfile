FROM java:6-jdk

ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8

# Installs Ant
ENV ANT_VERSION 1.9.11
RUN cd && \
    wget -q http://www.us.apache.org/dist//ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
    mkdir -p /opt/ant && \
    mv apache-ant-${ANT_VERSION}/** /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz
ENV ANT_HOME /opt/ant
ENV PATH ${PATH}:/opt/ant/bin


#############
# Ant Contrib
#############

# Preparation
ENV ANT_CONTRIB_VERSION 1.0b2

# Installation
RUN cd /tmp \
    && wget -q http://kent.dl.sourceforge.net/project/ant-contrib/ant-contrib/ant-contrib-${ANT_CONTRIB_VERSION}/ant-contrib-${ANT_CONTRIB_VERSION}-bin.tar.gz \
    && tar -zxf ant-contrib-${ANT_CONTRIB_VERSION}-bin.tar.gz \
    && cp ant-contrib/lib/ant-contrib.jar ${ANT_HOME}/lib \
    && rm -rf ant-contrib \
    && rm ant-contrib-${ANT_CONTRIB_VERSION}-bin.tar.gz \
    && unset ANT_CONTRIB_VERSION