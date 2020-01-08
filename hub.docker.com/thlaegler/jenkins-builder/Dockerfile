FROM gcr.io/cloud-builders/gcloud

LABEL maintainer "thlaegler"
LABEL package "io.laegler.builder"
LABEL namespace "cloudbuilder"
LABEL version "0.0.1-SNAPSHOT"

ENV GOOGLE_PROJECT_ID "xm-development"
ENV GOOGLE_APPLICATION_CREDENTIALS "service-account.json"
ENV GOOGLE_CLUSTER_NAME "platform-cluster"
ENV GOOGLE_CLUSTER_TIMEZONE "australia-southeast1-c"
ENV GOOGLE_CLUSTER_REGION "australia-southeast1"
ENV GIT_USEREMAIL "test@test.com"
ENV GIT_USERNAME "test"
ENV GIT_PASSWORD "test"

ENV DOCKER_VERSION "17.12.0~ce-0~ubuntu"
ENV DOCKER_SHA "0EBFCD88"
ENV PYTHON_VERSION "3.6.0"
ENV HELM_VERSION "2.9.0"
ENV MAVEN_VERSION "3.5.0"
ENV MAVEN_USER_HOME_DIR "/root"
ENV MAVEN_SHA "beb91419245395bd69a4a6edad5ca3ec1a8b64e41457672dc687c173a495f034"
ENV MAVEN_BASE_URL "https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries"
ENV M2_HOME "/usr/share/maven"
ENV JAVA_HOME "/usr/lib/jvm/java-8-openjdk-amd64/"
ENV JAVA_OPTS "-server -XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap -XX:+UseParallelGC -XX:MetaspaceSize=64m -XX:MaxMetaspaceSize=128m"
ENV CLASSPATH "$JAVA_HOME/lib/tools.jar"
ENV HELM_FILENAME "helm-v${HELM_VERSION}-linux-amd64.tar.gz"
ENV DOCKER_HOST "tcp://localhost:2375"
ENV PYENV_ROOT "/root/.pyenv"
ENV PATH "$PATH:$M2_HOME/bin:$JAVA_HOME/bin:/builder/google-cloud-sdk/bin/:$PYENV_ROOT/bin:$PATH"

# Additional Repos
RUN apt-get -y update && \
	apt-get install --no-install-recommends -qqy --force-yes curl wget apt-transport-https build-essential software-properties-common python-software-properties && \
	curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
	apt-key fingerprint ${DOCKER_SHA} && \
	add-apt-repository \
		"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
		$(lsb_release -cs) \
		stable" && \
	add-apt-repository ppa:openjdk-r/ppa && \
	wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add - && \
	echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list

RUN apt-get update -qqy && \
	apt-get install --no-install-recommends -qqy --force-yes \
		ca-certificates \
		ca-certificates-java \
		rsync \
		vim \
		maven \
		jq \
		git \
		ant \
		perl \
		openjdk-8-jdk \
		gnupg2 \
		libssl-dev \
		libbz2-dev \
		libreadline-dev \
		libsqlite3-dev \
		libffi-dev \
		libxml2 \
		libxml2-dev \
		libxml-libxml-perl \
		libwww-perl \
		liblwp-protocol-https-perl \
		python-dev \
		python3-pip \
		docker-ce=${DOCKER_VERSION} \
		jenkins && \
	apt-get clean && \
	update-ca-certificates -f && \
	rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/*

# GIT
RUN git config --global user.name ${GIT_USERNAME} && \
	git config --global user.email ${GIT_USEREMAIL} && \
	git config --global core.editor vim && \
	git config --system credential.helper gcloud.sh
	
# ANT

# JAVA

# MAVEN
#RUN mkdir -p /usr/share/maven /usr/share/maven/ref && \
#	curl -fsSL -o /tmp/apache-maven.tar.gz ${MAVEN_BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz && \
#	echo "${SHA} /tmp/apache-maven.tar.gz" | sha256sum -c - && \
#	tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 && \
#	rm -f /tmp/apache-maven.tar.gz && \
#	ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
COPY settings.xml ${M2_HOME}/settings.xml

# DOCKER

# PYTHON
#RUN apt-get update && apt-get install -qy virtualenv virtualenvwrapper
#RUN virtualenv venv -p python3
RUN pip install pip --upgrade && \
	curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash && \
	eval "$(pyenv init -)" && \
	eval "$(pyenv virtualenv-init -)" && \
	pyenv update && \
	pyenv install ${PYTHON_VERSION}

# KUBECTL

# HELM
RUN wget https://storage.googleapis.com/kubernetes-helm/${HELM_FILENAME} -P /tmp && \
	tar -zxvf /tmp/${HELM_FILENAME} -C /tmp && \
	mv /tmp/linux-amd64/helm /usr/local/bin && \
	rm -rf /tmp/${HELM_FILENAME}

# GCLOUD
#gcloud auth login
#gcloud config set container/use_application_default_credentials true
#gsutil -m cp gs://${GOOGLE_BUCKET_CLOUDBUILD}/${GOOGLE_SERVICE_ACCOUNT_FILE} service-account.json
#export GOOGLE_APPLICATION_CREDENTIALS=service-account.json
#RUN gcloud config set project ${GOOGLE_PROJECT_ID} && \
#	gcloud auth activate-service-account --key-file builder-sa.json || die "unable to authenticate service account for gcloud" && \
#	gcloud container clusters get-credentials ${GOOGLE_CLUSTER_NAME} --zone ${GOOGLE_CLUSTER_TIMEZONE} --project ${GOOGLE_PROJECT_ID} && \

# JMETER
RUN wget -c http://www-us.apache.org/dist//jmeter/binaries/apache-jmeter-4.0.tgz && \
	tar -zxvf apache-jmeter-4.0.tgz && \
	rm -rf apache-jmeter-4.0.tgz

ENTRYPOINT ["/bin/bash"] 