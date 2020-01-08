FROM		hauptmedia/java:oracle-java7

ENV     	DEBIAN_FRONTEND noninteractive

ENV		HADOOP_VERSION		2.6.0
ENV		HADOOP_INSTALL_DIR	/opt/hadoop

# install needed debian packages & clean up
RUN		apt-get update && \
		apt-get install -y --no-install-recommends curl tar ca-certificates && \
		apt-get clean autoclean && \
        	apt-get autoremove --yes && \
        	rm -rf /var/lib/{apt,dpkg,cache,log}/

# download and extract hadoop 
RUN		mkdir -p ${HADOOP_INSTALL_DIR} && \
		curl -L --silent  http://www.eu.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz | tar -xz --strip=1 -C ${HADOOP_INSTALL_DIR}

WORKDIR		${HADOOP_INSTALL_DIR}

