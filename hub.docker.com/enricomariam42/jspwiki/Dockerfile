#
#  Dockerfile for JSPWiki
#

FROM tomcat:8-jre8-alpine
MAINTAINER Enrico Maria Carmona, e.carmona@asst-monza.it

RUN apk add --update --no-cache busybox-suid curl tar unzip

ARG jspwiki_version=2.10.5
# jspwiki_version=`curl -s http://repo1.maven.org/maven2/org/apache/jspwiki/jspwiki-war/maven-metadata.xml | grep -o '<release>.*' | grep -o [0-9\.]*`
ENV JSPWIKI_VERSION=$jspwiki_version

ARG userid=1111
ARG groupid=1111
ARG user=jspwiki
ENV USER=$user

ARG jspwiki_binary_url=https://search.maven.org/remotecontent?filepath=org/apache/jspwiki/jspwiki-war/${jspwiki_version}/jspwiki-war-${jspwiki_version}.war
ARG wikipages_filename=jspwiki-wikipages-it-${jspwiki_version}
ARG wikipages_url=http://apache.panu.it/jspwiki/${jspwiki_version}/wikipages/jspwiki-wikipages-it-${jspwiki_version}.zip
ARG TF=/tmp/jspwikipages-download.zip
# ARG CATALINA_HOME=/usr/local/tomcat
ARG jspwiki_dir=/var/jspwiki
ENV JSPWIKI_DIR=$jspwiki_dir

# set default environment entries to configure jspwiki
ENV LANG=en_US.UTF-8 \
    CATALINA_OPTS=-Djava.security.egd=file:/dev/./urandom \
    HOME=/home/$USER \
    jspwiki_fileSystemProvider_pageDir=$JSPWIKI_DIR/pages \
    jspwiki_workDir=$JSPWIKI_DIR/work

# add unprivileged user 
RUN addgroup -g $groupid $USER && \
    adduser -D -u $groupid -G $USER $USER && \
#
#-------------------------------------------------------------
#  Install JSPWiki
#-------------------------------------------------------------
#
# add jspwiki war, create JSPWiki webapps dir, unzip it there.
# create a directory where all jspwiki stuff will live
    mkdir ${JSPWIKI_DIR} && \
# create subdirectories where all jspwiki stuff will live
    cd ${JSPWIKI_DIR} && mkdir pages logs etc work && \
# download last build
    wget -O /tmp/jspwiki.war ${jspwiki_binary_url} && \
# first remove default tomcat applications, we dont need them to jspwiki
    cd ${CATALINA_HOME}/webapps && rm -rf examples host-manager manager docs ROOT && \
    mkdir -p ${CATALINA_HOME}/webapps/ROOT && \
    unzip -q -d ${CATALINA_HOME}/webapps/ROOT /tmp/jspwiki.war && \
    rm /tmp/jspwiki.war && \
# download the default set of pages
    wget -O ${TF} ${wikipages_url} && \
    unzip -q -d /tmp ${TF} && \
    mv /tmp/${wikipages_filename}/*  ${JSPWIKI_DIR}/pages && \
    rm -r ${TF} /tmp/${wikipages_filename}

# Copy the init script
COPY run.sh /home/${USER}/run.sh
RUN chmod +x /home/${USER}/run.sh

# sets proper permissions
RUN chown -R $USER:$USER ${CATALINA_HOME}/* ${JSPWIKI_DIR}

CMD ["sh", "-c", "/home/${USER}/run.sh"]
