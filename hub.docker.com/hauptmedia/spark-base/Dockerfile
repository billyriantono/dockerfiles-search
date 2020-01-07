FROM		hauptmedia/java:oracle-java7

ENV     	DEBIAN_FRONTEND noninteractive

ENV		SPARK_VERSION		1.2.1	
ENV		SPARK_INSTALL_DIR	/opt/spark

# install needed debian packages & clean up
RUN		apt-get update && \
		apt-get install -y --no-install-recommends curl tar ca-certificates && \
		apt-get clean autoclean && \
        	apt-get autoremove --yes && \
        	rm -rf /var/lib/{apt,dpkg,cache,log}/

# download and extract spark 
RUN		mkdir -p ${SPARK_INSTALL_DIR} && \
		curl -L --silent http://d3kbcqa49mib13.cloudfront.net/spark-${SPARK_VERSION}-bin-hadoop2.4.tgz | tar -xz --strip=1 -C ${SPARK_INSTALL_DIR}

WORKDIR		${SPARK_INSTALL_DIR}

