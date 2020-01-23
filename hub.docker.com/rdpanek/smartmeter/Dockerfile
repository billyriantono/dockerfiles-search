FROM openshift/base-centos7
LABEL maintainer="rdpanek@gmail.com"

ENV SMARTMETER_VERSION 1.8.2
ENV SMARTMETER SmartMeter_${SMARTMETER_VERSION}_linux
ENV MIRROR_LINK http://smartmeter-api.etnetera.cz/download/release/${SMARTMETER_VERSION}/linux/full/${SMARTMETER}.zip
ENV SMARTMETER_HOME /opt/${SMARTMETER}
ENV JMETER_LIB ${SMARTMETER_HOME}/programs/apache-jmeter/lib
ENV ELASTIC_PLUGIN_LINK https://raw.githubusercontent.com/rdpanek/elasticsearch-backend-listener/2.1/install.sh

STOPSIGNAL SIGKILL

# Install SmartMeter
RUN yum install -y \
		curl \
		unzip && \
		yum clean all && \
		cd /opt/ && \
		curl -L -O ${MIRROR_LINK} && \
		unzip ${SMARTMETER}.zip -d . && rm -rf ${SMARTMETER}.zip && \
		# Install JMeter Plugins
		mkdir /opt/temp_plugins && cd /opt/temp_plugins && \
		curl -L -O https://jmeter-plugins.org/files/packages/jpgc-dummy-0.2.zip && \
		unzip -o -d /opt/temp_plugins jpgc-dummy-0.2.zip && \
		curl -L -O https://jmeter-plugins.org/files/packages/jpgc-casutg-2.6.zip && \
		unzip -o -d /opt/temp_plugins jpgc-casutg-2.6.zip && \
		# Copy plugins to jmeter enviroment
		cp lib/*.jar ${JMETER_LIB}/ && \
		cp lib/ext/*.jar ${JMETER_LIB}/ext/ && \
		rm -rf /opt/temp_plugins && \
		# Install ElasticSearchBackendListenerClient
		cd ${JMETER_LIB} && \
		curl -L -o install.sh $ELASTIC_PLUGIN_LINK && \
		chmod +x install.sh && ./install.sh && rm -rf install.sh && \
		#
		# SmartMeter contains /lib/jackson-core-2.9.5.jar, JMeter not
		rm -rf jackson-core-2.8.11.jar && \
		#
		PATH=$PATH:$SMARTMETER_HOME && export PATH && echo $PATH && \
		# custom settings
		echo 'etn_licence_file=/smartmeter/licence.bin' >> $SMARTMETER_HOME/custom/smartmeter.properties && \
		echo 'etn_reports_path=/smartmeter' >> $SMARTMETER_HOME/custom/smartmeter.properties && \
		echo 'etn_results_path=/smartmeter' >> $SMARTMETER_HOME/custom/smartmeter.properties && \
		echo 'etn_tests_path=/smartmeter' >> $SMARTMETER_HOME/custom/smartmeter.properties && \
		#
		mkdir /smartmeter && \
		# forward logs to docker log
		ln -sf /dev/stdout $SMARTMETER_HOME/logs/controller.log && \
		ln -sf /dev/stdout $SMARTMETER_HOME/logs/launcher.log

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

WORKDIR /smartmeter
ENTRYPOINT ["/docker-entrypoint.sh"]
