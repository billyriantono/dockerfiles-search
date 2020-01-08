# Copyright 2014-2015 Jahn Bertsch
# Copyright 2015 TOMORROW FOCUS News+ GmbH
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
# 
# http://www.apache.org/licenses/LICENSE-2.0
# 
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# build usergrid from source

FROM dlsimg/base-tomcat7

ARG ENV=production


ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# build usergrid
WORKDIR /root
ENV USERGRID_GIT_HASH 9fae8037a4b881e9c13a5a1f23f71dc34e950c40
#ENV USERGRID_GIT_HASH bd2385d76c3343d96b3b8648d1f68904e2247ed7
# cd usergrid && \
# RUN grep -rl log4j.rootLogger=INFO stack | xargs sed -i 's#log4j.rootLogger=INFO#log4j.rootLogger=WARN#g' 
# this is done in one run step so less files are included in the layers of the
# docker image, making it smaller.
RUN echo "+++ install packages required for compilation" && \
    apt-get update && \
    apt-get install -y maven curl jq git-core && \
    apt-get install -y python3-pip  && \
    pip3 install awscli && \
    \
    echo "+++ get usergrid source, set logging level" && \
    git clone https://github.com/apache/usergrid-java.git usergrid-java && \
    git clone https://github.com/deshbirc/usergrid.git usergrid && \
    \
    echo "+++ build usergrid" && \
    cd /root/usergrid-java && \
    mvn clean install -DskipTests && \
    cd /root/usergrid/stack && \
    git checkout $USERGRID_GIT_HASH && \    
    mvn clean install -DskipTests && \
    \ 
    echo "+++ cleanup" && \
    rm -rf /var/lib/tomcat7/webapps/ROOT && \  
    mv /root/usergrid/stack/rest/target/ROOT.war /var/lib/tomcat7/webapps && \
    mv /root/usergrid/stack/config/src/main/resources/usergrid-default.properties /usr/share/tomcat7/lib/usergrid-deployment.properties && \
    apt-get purge --auto-remove -y maven git-core ant && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /root/usergrid

# Default configuration
COPY usergrid-default.properties /usr/share/tomcat7/lib/usergrid-deployment.properties

# default command when starting container with "docker run"
CMD /root/run.sh

# exposed ports:
#  8080 usergrid http interface
#  8443 usergrid https interface
EXPOSE 8080 8443

# runtime configuration script: since this is updated frequently during development, add it last
COPY run.sh /root/run.sh
