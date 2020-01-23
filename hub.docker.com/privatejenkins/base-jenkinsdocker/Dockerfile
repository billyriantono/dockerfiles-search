FROM jenkins
# if we want to install via apt
COPY plugins.txt /usr/share/jenkins/plugins.txt
COPY plugins2.txt /usr/share/jenkins/plugins2.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins2.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
USER root
#Add OpenJdk repo
RUN echo deb http://http.debian.net/debian jessie-backports main >> /etc/apt/sources.list
#Install 3rd party
RUN apt-get update -qq && apt-get install -qqy \
    git-core \
    nodejs \
    npm \
    vim

#    software-properties-common \
#    python-software-properties \	 
	
RUN apt-get install -qqy \    
	net-tools \
	tofrodos \
	maven \
	ruby-dev \
	ruby
	
#RUN add-apt-repository --yes ppa:openjdk-r/ppa

#RUN apt-get update
RUN apt-get install -y openjdk-7-jdk
RUN apt-get install -y openjdk-8-jdk
RUN ln -s /usr/bin/fromdos /usr/bin/dos2unix

#install Chromium
#RUN apt-get update && apt-get install -y xvfb chromium-browser

#ADD xvfb-chromium /usr/bin/xvfb-chromium
#RUN ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome
#RUN ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser
#UI installs
RUN ln -s /usr/bin/nodejs /usr/bin/node
RUN npm install -g grunt-cli@1.2.0
RUN npm install -g bower@1.7.9
#RUN npm install -g phantomjs-prebuilt
RUN npm install -g phantomjs@1.9.18
#RUN gem update --system
RUN gem install compass

#Install nodejs6
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash
RUN apt-get install -qqy nodejs

#Install docker
#RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
#RUN echo deb http://apt.dockerproject.org/repo ubuntu-trusty main >/etc/apt/sources.list.d/docker.list
#RUN apt-get update
#RUN apt-get install -y docker-engine
# Install Docker from Docker Inc. repositories.

#RUN curl -sSL https://get.docker.com/ | sh
#RUN echo export http_proxy="http://web-proxy.il.hpecorp.net:8080/" >> /etc/default/docker
#RUN echo export https_proxy="http://web-proxy.il.hpecorp.net:8080/" >> /etc/default/docker
#RUN echo DOCKER_OPTS="\"--insecure-registry myd-vm02816.hpswlabs.adapps.hp.com:5000\"" >> /etc/default/docker

# Define additional metadata for our image.
#VOLUME /var/lib/docker

#RUN service docker start
#RUN gem install compass:0.12.2
#Edit hosts file
#RUN cat /etc/hosts |sed 's/localhost/localhost mydev.devdomain.com/'>/etc/hosts
RUN cat /etc/bash.bashrc |sed "s/PS1='/PS1='Docker_/" | tee /etc/bash.bashrc
RUN echo "cd /var/jenkins_home" >> /etc/bash.bashrc


#Configure Jenkins
COPY bin/ /var/jenkins_home/bin/
COPY resources/proxy.xml /var/jenkins_home/proxy.xml
COPY resources/config.xml /var/jenkins_home/config.xml
COPY resources/credentials.xml /var/jenkins_home/credentials.xml
COPY resources/hudson.tasks.Maven.xml /var/jenkins_home/hudson.tasks.Maven.xml
COPY resources/hudson.maven.MavenModuleSet.xml /var/jenkins_home/hudson.maven.MavenModuleSet.xml
#COPY resources/jobs /var/jenkins_home/jobs
#COPY resources/SUN/JDK/1.7.0_51/linux64 /var/jdk/1.7.0_51
#COPY resources/SUN/JDK/1.8.0_51/linux64 /var/jdk/1.8.0_51
#COPY resources/java-1.8.0-openjdk-amd64 /usr/lib/jvm/java-1.8.0-openjdk-amd64
#COPY resources/Apache/maven/3.0.3/multi-platform /var/maven/3.0.3
#COPY resources/plugins /var/jenkins_home/plugins
RUN ln -s /usr/lib/jvm/java-1.8.0-openjdk-amd64 /usr/lib/jvm/java-1.8.0-openjdk
RUN rm -rf /var/jenkins_home/credentials.xml
#COPY bin/installDocker.sh /var/jenkins_home/bin/installDocker.sh
#COPY bin/runNewRedis.sh /var/jenkins_home/bin/runNewRedis.sh
#COPY bin/runNewDockerRegistry.sh /var/jenkins_home/bin/runNewDockerRegistry.sh
#RUN service docker restart
#RUN /var/jenkins_home/bin/runNewRedis.sh
#RUN chown -R jenkins:jenkins /var/jenkins_home

#USER jenkins
# drop back to the regular jenkins user - good practice
ENV http_proxy="http://web-proxy.il.hpecorp.net:8080/"
ENV https_proxy="http://web-proxy.il.hpecorp.net:8080/"
ENV no_proxy="127.0.0.1,localhost,hpeswlab.net,mydyumserver,mydyumserver.hpswlabs.adapps.hp.com,*.hp.com,16.59.0.0,hpswlabs.adapps.hp.com:80"
#ENV M2_HOME="/usr/share/maven"
#ENV M2="/usr/share/maven"
#ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk
RUN sed -i 's# <proxies># <proxies>\n    <proxy>\n        <id>HPQNETPROXY</id>\n        <active>true</active>\n        <host>web-proxy.bbn.hpecorp.net</host>\n        <port>8080</port>\n        <nonProxyHosts>*.devlab.ad</nonProxyHosts>\n    </proxy>\n#' /usr/share/maven/conf/settings.xml