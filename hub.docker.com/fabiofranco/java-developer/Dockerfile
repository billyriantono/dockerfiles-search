FROM openjdk:8

RUN apt-get update -qq && \
	apt-get install ftp unzip unrar-free locales tree vim htop git subversion build-essential sudo ssh libgtk-3-0 libxtst-dev python-setuptools python-dev groff build-essential -qq && \
	\
	export dev_home=/home/developer && \
	mkdir ${dev_home} && \
	useradd -U -u 1000 -d ${dev_home} -s /bin/bash developer && \
	chown -R 1000:1000 ${dev_home} && \
	echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
	chmod 0440 /etc/sudoers.d/developer && \
	locale-gen en_US.UTF-8 && \
	\
	apt-get autoclean -qq && \
	apt-get autoremove -qq && \
	rm -rf /var/lib/apt/lists/* && \
	\
	easy_install pip && pip install awscli --upgrade && \
	\
	curl -L -o ${dev_home}/maven.tar.gz "http://www-us.apache.org/dist/maven/maven-3/3.5.3/binaries/apache-maven-3.5.3-bin.tar.gz" && \
	tar zxf ${dev_home}/maven.tar.gz -C /opt && \
	rm ${dev_home}/maven.tar.gz && \
	ln -s /opt/apache-maven-3.5.3/bin/mvn /bin/mvn

USER developer
VOLUME /home/developer/isolation
WORKDIR /home/developer
ENTRYPOINT /bin/bash
