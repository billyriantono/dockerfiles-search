# howto call: docker build -t dwd_pdi:latest -f Dockerfile .

FROM debian:8

MAINTAINER Djordja Markovic <djordja.markovic@it-novum.com>

ENV JVM_PATH=/usr/lib/jvm \
	JAVA_VERSION=jdk1.8.0_212 \
	JAVA_FILENAME=jdk-8-linux-x64 \
	JAVA_DOWNLOAD_LINK="https://github.com/frekele/oracle-java/releases/download/8u212-b10/jdk-8u212-linux-x64.tar.gz" \
	PDI_VERSION=8.0 \
	PDI_BUILD=8.0.0.0-28 \ 
	PENTAHO_HOME=/opt/pentaho 

# change to jvm directory
WORKDIR $JVM_PATH

RUN apt-get update \
    && apt-get install -y \
    	bash \
	  	tree \
	  	wget \
		unzip \
	  	sudo \
	  	vim \
	  	iputils-ping \
	  	less \
	  	vim && \
	  	\
		#install java
		wget --quiet --no-cookies --no-check-certificate "${JAVA_DOWNLOAD_LINK}" -O $JAVA_FILENAME.tar.gz && \
		tar -xf $JAVA_FILENAME.tar.gz && \
		rm $JAVA_FILENAME.tar.gz  \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
	# create PENTAHO_HOME
	&& mkdir -p ${PENTAHO_HOME} \
	# add rights
	&& chmod -R 777 /tmp

# download software
RUN wget -O /tmp/pdi-ce-${PDI_BUILD}.zip "https://sourceforge.net/projects/pentaho/files/Pentaho%20${PDI_VERSION}/client-tools/pdi-ce-${PDI_BUILD}.zip/download"

# add folder share
VOLUME "/share"

# add JAVA_HOME and PATH
#ENV LANG='en_US.UTF-8' LANGUAGE='en_US.UTF-8' LC_ALL='en_US.UTF-8'
#ENV JAVA_HOME="/usr/lib/jvm/jdk1.8.0_212"
ENV JAVA_HOME="${JVM_PATH}/${JAVA_VERSION}"
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# extract software and remove zip
RUN unzip -q "/tmp/pdi-ce-${PDI_BUILD}" -d $PENTAHO_HOME \
	&& ls -ltrah $PENTAHO_HOME/data-integration \
	&& rm -fv /tmp/pdi-ce-${PDI_BUILD}.zip

# change to PENTAHO_HOME directory
WORKDIR $PENTAHO_HOME
