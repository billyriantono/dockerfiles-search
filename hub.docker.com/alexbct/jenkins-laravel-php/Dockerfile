FROM debian:jessie

#
#Install Java
ENV LANG="C.UTF-8" \
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64" \
JAVA_VERSION="8u91" \
JAVA_DEBIAN_VERSION="8u91-b14-1~bpo8+1" \
DEBIAN_FRONTEND="noninteractive" \
CA_CERTIFICATES_JAVA_VERSION="20140324"

# see https://bugs.debian.org/775775
# and https://github.com/docker-library/java/issues/19#issuecomment-70546872
# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
#RUN apt-add-repository ppa:ondrej/php -y && apt-add-repository ppa:fkrull/deadsnakes-python2.7 -y
#RUN echo 'deb http://httpredir.debian.org/debian jessie-backports main' > /etc/apt/sources.list.d/jessie-backports.list
#http://httpredir.debian.org/demo.html because mirror redirect does not always work
RUN echo 'deb http://mirrors.accretive-networks.net/debian/ jessie-backports main' >> /etc/apt/sources.list.d/jessie-backports.list \
	&& echo 'deb http://mirrors.kernel.org/debian/ jessie-backports main' >> /etc/apt/sources.list.d/jessie-backports.list \
	&& apt-get clean && apt-get update \
	&& apt-get install -y --force-yes --no-install-recommends --fix-missing \
	software-properties-common \
	ca-certificates \
	curl \
	wget \
	bzr \
	git \
	mercurial \
	openssh-client \
	subversion \
	procps \
	bzip2 \
	zip \
	unzip \
	xz-utils \
	ant \
	php5-cli \
	php-codecoverage \
	phpunit \
	phploc \
	php-codesniffer \
	pdepend \
	phpmd \
	phpcpd \
	phpdox \
	build-essential \
	fail2ban \
	gcc \
	libmcrypt4 \
	libpcre3-dev \
	make \
	python2.7 \
	python-pip \
	supervisor \
	ufw unattended-upgrades \
	whois \
	zsh \
	php5-gd \
	php5-curl \
	php5-mysql \
	libxrender1 \
	pwgen \
	#&& pip install httpie \

	&& { \
	echo '#!/bin/sh'; \
	echo 'set -e'; \
	echo; \
	echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home \
	&& set -x \
	   
	##&& apt-get update \
	&& apt-get install -y \
	openjdk-8-jdk="$JAVA_DEBIAN_VERSION" \
	ca-certificates-java="$CA_CERTIFICATES_JAVA_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ] \
	# see CA_CERTIFICATES_JAVA_VERSION notes above
	&& /var/lib/dpkg/info/ca-certificates-java.postinst configure

# Jenkins
#ARG user=jenkins 
#ARG group=jenkins 
#ARG uid=1000 
#ARG gid=1000 
#ARG JENKINS_VERSION 
#ARG JENKINS_SHA

ENV JENKINS_HOME="/var/jenkins_home" \
JENKINS_SLAVE_AGENT_PORT="50000" \
APP_DIRECTORY="/home/forge" \
TINI_SHA="066ad710107dc7ee05d3aa6e4974f01dc98f3888" \
JENKINS_VERSION="${JENKINS_VERSION:-1.651.3}" \
JENKINS_SHA="${JENKINS_SHA:-564e49fbd180d077a22a8c7bb5b8d4d58d2a18ce}" \
JENKINS_UC="https://updates.jenkins.io" \
COPY_REFERENCE_FILE_LOG="$JENKINS_HOME/copy_reference_file.log" \
user=jenkins \
group=jenkins \
uid=1000 \
gid=1000 


# Jenkins is run with user `jenkins`, uid = 1000
# If you bind mount a volume from the host or a data container, 
# ensure you use the same uid
RUN groupadd -g ${gid} ${group} \
	&& useradd -d "$JENKINS_HOME" -u ${uid} -g ${gid} -m -s /bin/bash ${user} \
	# `/usr/share/jenkins/ref/` contains all reference configuration we want 
	# to set on a fresh new installation. Use it to bundle additional plugins 
	# or config file with your custom jenkins Docker image.
	&& mkdir -p /usr/share/jenkins/ref/init.groovy.d \
	&& [ -f "$APP_DIRECTORY" ]  && echo "directory already exists"  || mkdir -p "$APP_DIRECTORY" \

	# Use tini as subreaper in Docker container to adopt zombie processes 
	&& curl -fsSL https://github.com/krallin/tini/releases/download/v0.5.0/tini-static -o /bin/tini && chmod +x /bin/tini \
	&& echo "$TINI_SHA  /bin/tini" | sha1sum -c - \

	&& curl -fsSL http://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war -o /usr/share/jenkins/jenkins.war \
	&& echo "$JENKINS_SHA  /usr/share/jenkins/jenkins.war" | sha1sum -c -

	# Jenkins home directory is a volume, so configuration and build history 
	# can be persisted and survive image upgrades



# 8080 for main web interface 50000 will be used by attached slave agents

USER ${user}

#This will not work because the $JENKINS_HOME directory is attached as a volume
RUN [ -f $JENKINS_HOME/.ssh/id_rsa ] && echo "ssh key already exists" || ssh-keygen -b 2048 -t rsa -f $JENKINS_HOME/.ssh/id_rsa -q -N ""
#RUN mkdir -p $JENKINS_HOME/.ssh
RUN touch $JENKINS_HOME/.ssh/known_hosts
RUN ssh-keyscan -T 60 -H github.com >> $JENKINS_HOME/.ssh/known_hosts
RUN ssh-keyscan -T 60 -H bitbucket.org >> $JENKINS_HOME/.ssh/known_hosts
#RUN ssh-keyscan -T 60 bitbucket.org >> $JENKINS_HOME/.ssh/known_hosts

VOLUME /var/jenkins_home

USER root
# from a derived Dockerfile, can use `RUN plugins.sh active.txt` to setup /usr/share/jenkins/ref/plugins from a support bundle
COPY plugins.sh /usr/local/bin/plugins.sh
COPY install-plugins.sh /usr/local/bin/install-plugins.sh
COPY plugins.txt /usr/share/jenkins/plugins.txt
COPY jenkins.sh /usr/local/bin/jenkins.sh
COPY script.sh /usr/local/bin/script.sh
COPY init.groovy /usr/share/jenkins/ref/init.groovy.d/tcp-slave-agent-port.groovy

RUN chmod +x /usr/local/bin/jenkins.sh && chmod +x /usr/local/bin/plugins.sh && chmod +x /usr/local/bin/install-plugins.sh && chmod +x /usr/local/bin/script.sh \
	&& wget -O /usr/local/bin/composer https://getcomposer.org/composer.phar && chmod +x /usr/local/bin/composer \
	&& echo "xdebug.max_nesting_level = 200" >> /etc/php5/mods-available/xdebug.ini \
	&& chown -R ${user} "$JENKINS_HOME" /usr/share/jenkins/ref "$APP_DIRECTORY"

EXPOSE 8080 50000

#RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
#USER ${user}
##RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
##ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]

#PHP
#USER root

# ENV GOSU_VERSION 1.7
# RUN set -x \
# 	&& apt-get update && apt-get install -y --no-install-recommends ca-certificates wget \
# 	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
# 	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
# 	&& export GNUPGHOME="$(mktemp -d)" \
# 	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
# 	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
# 	&& rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
# 	&& chmod +x /usr/local/bin/gosu \
# 	&& gosu nobody true 
	##&& apt-get purge -y --auto-remove ca-certificates wget

#INSTALL MYSQL
#RUN apt-get update && apt-get install -y perl pwgen --no-install-recommends

# gpg: key 5072E1F5: public key "MySQL Release Engineering <mysql-build@oss.oracle.com>" imported
#RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys A4A9406876FCBD3C456770C88C718D3B5072E1F5

ENV MYSQL_MAJOR="5.7" MYSQL_VERSION="5.7.13-1debian8"



RUN echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-${MYSQL_MAJOR}" > /etc/apt/sources.list.d/mysql.list \

# the "/var/lib/mysql" stuff here is because the mysql-server postinst doesn't have an explicit way to disable the mysql_install_db codepath besides having a database already "configured" (ie, stuff in /var/lib/mysql/mysql)
# also, we set debconf keys to make APT a little quieter
	&& { \
		echo mysql-community-server mysql-community-server/data-dir select ''; \
		echo mysql-community-server mysql-community-server/root-pass password ''; \
		echo mysql-community-server mysql-community-server/re-root-pass password ''; \
		echo mysql-community-server mysql-community-server/remove-test-db select false; \
	} | debconf-set-selections \
	# gpg: key 5072E1F5: public key "MySQL Release Engineering <mysql-build@oss.oracle.com>" imported
	&& apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys A4A9406876FCBD3C456770C88C718D3B5072E1F5 \
	&& apt-get update && apt-get install -y mysql-server="${MYSQL_VERSION}" \
	&& rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql /var/run/mysqld \
	&& chown -RL mysql:mysql /var/lib/mysql /var/run/mysqld \
# ensure that /var/run/mysqld (used for socket and lock files) is writable regardless of the UID our mysqld instance ends up having at runtime
	&& chmod 777 /var/run/mysqld \

# comment out a few problematic configuration values
# don't reverse lookup hostnames, they are usually another container
## set password expiration
	&& sed -Ei 's/^(bind-address|log)/#&/' /etc/mysql/my.cnf \
	&& echo 'skip-host-cache\nskip-name-resolve' | awk '{ print } $1 == "[mysqld]" && c == 0 { c = 1; system("cat") }' /etc/mysql/my.cnf > /tmp/my.cnf \
	&& mv /tmp/my.cnf /etc/mysql/my.cnf && echo "default_password_lifetime = 0" >> /etc/mysql/my.cnf && service mysql restart \
    && PASS=$(pwgen 12 1) \
    && echo "=> Creating MySQL user ${user} with $PASS password" \
    && echo "GRANT ALL ON *.* TO '${user}'@'%' IDENTIFIED BY '$PASS' WITH GRANT OPTION; FLUSH PRIVILEGES" | mysql \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

    # && sleep 10s\
    # && ps aux | grep mysql \
    # && cat /etc/mysql/my.cnf \
#&& find / -type s \
#&& mysql -uroot -e "CREATE USER '${user}'@'%' IDENTIFIED BY '$PASS';" 
#&& mysql -uroot -e "GRANT ALL PRIVILEGES ON *.* TO '${user}'@'%' WITH GRANT OPTION;" 

#mysql -uroot -e "CREATE USER 'blah'@'%' IDENTIFIED BY 'blah';"
#mysql --user="root"  -e "select * from mysql.user;"
#mysql -uroot -e "select * from mysql.user;"
VOLUME /var/lib/mysql

EXPOSE 3306

USER ${user}
ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]