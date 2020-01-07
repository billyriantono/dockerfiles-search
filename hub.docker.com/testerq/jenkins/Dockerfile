FROM jenkins/jenkins:alpine

ENV TZ=Asia/Shanghai

RUN install-plugins.sh robot ansible antisamy-markup-formatter build-timeout credentials-binding timestamper ws-cleanup  \
    workflow-aggregator pipeline-stage-view git ssh-slaves matrix-auth pam-auth ldap email-ext mailer subversion \
    analysis-collector analysis-core copy-to-slave copyartifact copy-data-to-workspace-plugin blueocean performance plot covcomplplot parameterized-trigger \
    jdk-tool command-launcher bouncycastle-api zap allure-jenkins-plugin nodelabelparameter hubot-steps config-file-provider ssh-agent \
    sonar ant gradle github-branch-source android-emulator open-stf jslint toolenv cloudbees-folder mashup-portlets-plugin pipeline-github-lib \
    localization-support localization-zh-cn locale artifactory gitlab-plugin ruby-runtime gitlab-hook

WORKDIR $JENKINS_HOME

USER root

# install jmeter
ARG JMETER_VERSION=5.1
ENV JMETER_HOME=/usr/local/jmeter
#ARG MD5_JMETER=fc83806c1f7546ca1b92040aea4d35de
RUN curl -fsSL -O https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz && \
#    echo "${MD5_JMETER}  apache-jmeter-${JMETER_VERSION}.tgz" | md5sum -c - && \
	   tar -xzf apache-jmeter-${JMETER_VERSION}.tgz && mv apache-jmeter-${JMETER_VERSION} ${JMETER_HOME} && \
     rm -rf apache-jmeter-${JMETER_VERSION}.tgz \
			${JMETER_HOME}/bin/examples \
			${JMETER_HOME}/bin/templates \
			${JMETER_HOME}/bin/*.cmd \
			${JMETER_HOME}/bin/*.bat \
			${JMETER_HOME}/docs \
			${JMETER_HOME}/printable_docs && \
    sed -i "s/# RUN_IN_DOCKER/RUN_IN_DOCKER/g" $JMETER_HOME/bin/jmeter
    
# install plugins manager
RUN curl -LO http://search.maven.org/remotecontent?filepath=kg/apc/cmdrunner/2.2/cmdrunner-2.2.jar && \
	mv cmdrunner-2.2.jar $JMETER_HOME/lib && \
	curl -LO http://search.maven.org/remotecontent?filepath=kg/apc/jmeter-plugins-manager/1.3/jmeter-plugins-manager-1.3.jar && \
	mv jmeter-plugins-manager-1.3.jar $JMETER_HOME/lib/ext && \
	java -cp $JMETER_HOME/lib/ext/jmeter-plugins-manager-1.3.jar org.jmeterplugins.repository.PluginManagerCMDInstaller

COPY *.properties ${JMETER_HOME}/bin/
COPY rmi_keystore.jks ${JMETER_HOME}/bin/
COPY m2u.jar $JAVA_HOME/lib/
COPY j2u /usr/bin/

# install allure
ARG ALLURE_VERSION=2.7.0
ENV ALLURE_HOME=/usr/local/allure-${ALLURE_VERSION}
ARG SHA_ALLURE=0ff4e7f913428e3d519e08edf597ade171922f8d71925eb4ae975eafb84929a0            
RUN curl -fsSL -O https://dl.bintray.com/qameta/generic/io/qameta/allure/allure/${ALLURE_VERSION}/allure-${ALLURE_VERSION}.tgz && \
    echo "${SHA_ALLURE}  allure-${ALLURE_VERSION}.tgz" | sha256sum -c - && \
	tar -xzf allure-${ALLURE_VERSION}.tgz -C /usr/local/ && \
    rm -f allure-${ALLURE_VERSION}.tgz 
    
# install bzt
RUN apk add --no-cache python3 libxml2 libxslt vim && \
    ln -s /usr/bin/pip3 /usr/bin/pip && \
    apk add --no-cache gcc libxml2-dev libc-dev python3-dev libxslt-dev linux-headers && \
    pip install --no-cache-dir -U pip && \ 
    pip install --no-cache-dir bzt     
# 修改一个中文显示的bug
#   && \ sed -i "s/return text./return text #./g" /usr/lib/python2.7/site-packages/bzt/modules/reporting.py

# install ansible and kubectl
RUN  apk add --no-cache libffi-dev openssl-dev make && \ 
     pip install --no-cache-dir ansible pycrypto && \
     curl -L https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl \
          -o /usr/local/bin/kubectl && \
     chmod +x /usr/local/bin/kubectl && \
     apk del gcc libxml2-dev libc-dev python3-dev libxslt-dev linux-headers make libffi-dev openssl-dev

# set path
ENV PATH=${ALLURE_HOME}/bin:${JMETER_HOME}/bin:${PATH}

#USER jenkins

EXPOSE 8080

HEALTHCHECK --interval=5m --timeout=3s \
  CMD curl -f http://localhost:8080/login || exit 1

    
        
