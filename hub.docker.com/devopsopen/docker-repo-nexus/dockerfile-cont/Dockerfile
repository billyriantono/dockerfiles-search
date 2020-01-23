FROM ubuntu

# Install needs
RUN apt-get update \
	&& apt-get -q -y -f install \
				wget \
				default-jdk \
				telnet \
				iputils-ping

# Install jmeter

RUN mkdir -p "/usr/share/jmeter/" \
	&& cd /tmp \
	&& wget -qc http://ftp.ps.pl/pub/apache//jmeter/binaries/apache-jmeter-3.1.tgz \
	&& tar -xf apache-jmeter-3.1.tgz --directory "/usr/share/jmeter" --strip-components=1 --no-same-owner \
	&& rm apache-jmeter-3.1.tgz \
	&& ln -s /usr/share/jmeter/bin/jmeter /usr/bin/jmeter

# Set Jmeter Home
ENV JMETER_HOME /usr/share/jmeter/bin/jmeter

# Add Jmeter to the Path
ENV PATH $JMETER_HOME/bin:$PATH
