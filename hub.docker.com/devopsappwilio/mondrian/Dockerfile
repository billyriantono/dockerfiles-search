FROM tomcat:8

RUN apt-get update
ADD mondrian-3.5.0.zip "/tmp/"
ADD conf.sh "/tmp/"
ADD conf_files.sh "/"
ADD postgresql-42.1.4.jar "/tmp/"
RUN cd "/tmp/" \
	&& chmod +x "/conf_files.sh" \
	&& chmod +x "/tmp/conf.sh" \
	&& mkdir -p "/tmp/mondrian/" \
	&& unzip  "/tmp/mondrian-3.5.0.zip" -d "/tmp/mondrian/" \
	&& mkdir -p "/usr/local/tomcat/webapps/mondrian" \
	&& unzip  "/tmp/mondrian/mondrian-3.5.0/lib/mondrian.war" -d "/usr/local/tomcat/webapps/mondrian" \
	&& cp "postgresql-42.1.4.jar" "/usr/local/tomcat/webapps/mondrian/WEB-INF/lib/" \
	&& bash "/tmp/conf.sh" \
	&& rm -rf "mondrian" \
	&& rm -rf "mondrian-3.5.0.zip" \
	&& rm -rf "conf.sh" \
	&& rm -rf "postgresql-42.1.4.jar"

CMD ["bash", "-c", "/conf_files.sh && catalina.sh run"]
