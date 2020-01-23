FROM java:openjdk-8u111-jdk

ENV	JMETER_VERSION 3.2
ENV	JMETER_HOME	/opt/jmeter
## use http://mirrors.tuna.tsinghua.edu.cn/apache/jmeter/binaries/apache-jmeter-3.2.tgz
ENV	JMETER_DOWNLOAD_URL http://mirrors.tuna.tsinghua.edu.cn/apache/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz

# install needed debian packages & clean up
RUN	apt-get update -y && \
    apt-get install -y --no-install-recommends curl tar ca-certificates unzip && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

# download and extract jmeter
RUN	mkdir -p ${JMETER_HOME} && \
    curl -L --silent ${JMETER_DOWNLOAD_URL} | tar -xz --strip=1 -C ${JMETER_HOME} && \
    curl -L --silent http://jmeter-plugins.org/downloads/file/JMeterPlugins-Standard-1.2.1.zip -o /tmp/jmeter-plugins-standard.zip && \
    unzip -o -d /opt/jmeter/ /tmp/jmeter-plugins-standard.zip && \
    rm /tmp/jmeter-plugins-standard.zip

WORKDIR	${JMETER_HOME}
