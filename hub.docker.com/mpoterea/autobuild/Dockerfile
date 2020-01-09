FROM ubuntu:latest
RUN apt-get update -q \
	&& apt-get install -qy \
		wget \
		openjdk-8-jre \
		xvfb \
		xz-utils \
		zip \
	&& apt-get clean -q \
	&& rm -rf /var/lib/apt/lists/*
ENV ARDUINO_IDE_VERSION 1.8.7
RUN (wget -qO- https://downloads.arduino.cc/arduino-${ARDUINO_IDE_VERSION}-linux64.tar.xz \
	| tar xJC /usr/local/share \
	&& ln -s /usr/local/share/arduino-${ARDUINO_IDE_VERSION} /usr/local/share/arduino \
	&& ln -s /usr/local/share/arduino-${ARDUINO_IDE_VERSION}/arduino /usr/local/bin/arduino)
RUN (wget -q https://sonarsource.bintray.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.2.0.1227-linux.zip)
ENV SONAR_SCANNER_VERSION 3.2.0.1227
RUN (unzip -qq sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip -d /usr/local/share \
	&& ln -s /usr/local/share/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux /usr/local/share/sonarscanner \
	&& ln -s /usr/local/share/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux/bin /usr/local/bin/sonarscanner)
COPY ./start-xvfb.sh /usr/local/bin/start-xvfb
ENV DISPLAY :1.0 COPY ./start-session.sh /usr/local/bin/start-session
CMD ["/bin/bash"]
ENTRYPOINT ["/usr/local/bin/start-session"]