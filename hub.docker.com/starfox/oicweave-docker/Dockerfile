FROM tomcat:7
MAINTAINER <sascha.herrmann@web.de>

# Download latest weave build from branch master and unzip
RUN 	mkdir -p /tmp && \
	wget -O /tmp/Weave.zip https://github.com/IVPR/Weave-Binaries/zipball/master && \
	cd /tmp && \
	unzip Weave.zip 
# Install latest weave build 
RUN 	cd /tmp && \
	cd `ls | grep WeaveTeam-` && \
	mv -vf ROOT/* /usr/local/tomcat/webapps/ROOT && \
	mv -vf WeaveServices.war /usr/local/tomcat/webapps/
# Optional cleanup
RUN	rm -rf /tmp/Weave*

	
